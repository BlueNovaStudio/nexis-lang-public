# 🏗️ Proyectos completos

Cinco proyectos pequeños pero reales. Cada uno combina structs o clases,
colecciones, funciones, control de flujo y manejo de errores, y su salida es
**determinista** (no depende del orden interno de `Map` ni de `Set`).

---

## 1. Inventario de una tienda

**Objetivo:** registrar productos, calcular el valor del inventario, vender y
reponer stock, y buscar productos por nombre.

**Conceptos:** `struct`, `Vector`, funciones con copia de salida, `lanzar` /
`catch`, ordenamiento manual.

```nexis
#inject Vector;

struct Producto {
    string nombre;
    int precio;
    int stock;
}

Vector<Producto> inventario = []

void agregar(string: nombre, int: precio, int: stock) -> void {
    inventario.add(Producto(nombre, precio, stock))
}

func indice_de(string: nombre) -> int {
    for i in 0 ... inventario.length() {
        if (inventario[i].nombre == nombre) {
            emit -> i
        }
    }
    emit -> -1
}

func buscar(string: nombre) -> Producto {
    int i = indice_de(nombre)
    if (i < 0) {
        lanzar ErrorValidacion("No existe el producto " + nombre)
    }
    emit -> inventario[i]
}

void vender(string: nombre, int: cantidad) -> void {
    int i = indice_de(nombre)
    if (i < 0) {
        lanzar ErrorValidacion("Producto desconocido: " + nombre)
    }
    if (inventario[i].stock < cantidad) {
        lanzar ErrorValidacion("Stock insuficiente de " + nombre)
    }
    Producto p = inventario[i]
    p.stock = p.stock - cantidad
    inventario[i] = p
}

void reponer(string: nombre, int: cantidad) -> void {
    int i = indice_de(nombre)
    if (i < 0) {
        lanzar ErrorValidacion("Producto desconocido: " + nombre)
    }
    Producto p = inventario[i]
    p.stock = p.stock + cantidad
    inventario[i] = p
}

func valor_total() -> int {
    int total = 0
    foreach (Producto p, inventario) {
        total = total + p.precio * p.stock
    }
    emit -> total
}

func unidades_totales() -> int {
    int total = 0
    foreach (Producto p, inventario) {
        total = total + p.stock
    }
    emit -> total
}

void ordenar_por_nombre(Vector<Producto>: lista) -> void {
    for i in 0 ... lista.length() - 1 {
        int mejor = i
        for j in i + 1 ... lista.length() {
            if (lista[j].nombre < lista[mejor].nombre) {
                mejor = j
            }
        }
        if (mejor != i) {
            Producto tmp = lista[i]
            lista[i] = lista[mejor]
            lista[mejor] = tmp
        }
    }
}

// --- programa ---
agregar("Arroz", 1500, 10)
agregar("Leche", 3200, 5)
agregar("Pan", 800, 20)

Console.println("productos: " + inventario.length())
Console.println("unidades: " + unidades_totales())
Console.println("valor: " + valor_total())

vender("Arroz", 3)
reponer("Leche", 2)
Console.println("tras mover stock: " + valor_total())

Producto p = buscar("Pan")
Console.println(p.nombre + " -> " + p.stock)

try {
    vender("Cafe", 1)
} catch (ErrorValidacion e) {
    Console.println("Error: " + e.mensaje())
}

try {
    vender("Pan", 999)
} catch (ErrorValidacion e) {
    Console.println("Error: " + e.mensaje())
}

ordenar_por_nombre(inventario)
foreach (Producto prod, inventario) {
    Console.println(fs"{prod.nombre}: {prod.stock} x {prod.precio}")
}
```

Salida:

```
productos: 3
unidades: 35
valor: 47000
tras mover stock: 48900
Pan -> 20
Error: Producto desconocido: Cafe
Error: Stock insuficiente de Pan
Arroz: 7 x 1500
Leche: 7 x 3200
Pan: 20 x 800
```

### Variante con `Map`

Si solo necesitas precio y stock, un `Map<string, int>` evita definir un
struct. El precio va en un mapa y el stock en otro.

```nexis
#inject Map;

Map<string, int> precios = {}
Map<string, int> stock = {}

void alta(string: nombre, int: precio, int: cantidad) -> void {
    precios.put(nombre, precio)
    stock.put(nombre, cantidad)
}

func valor() -> int {
    int total = 0
    foreach (clave in precios) {
        total = total + precios.get(clave) * stock.get(clave)
    }
    emit -> total
}

alta("Arroz", 1500, 10)
alta("Leche", 3200, 5)

Console.println(precios.contains("Arroz"))
Console.println(stock.get("Leche"))
Console.println(valor())
```

Salida:

```
true
5
31000
```

---

## 2. Agenda de contactos

**Objetivo:** alta, baja, búsqueda exacta y búsqueda por prefijo, con
validación de duplicados.

**Conceptos:** `struct`, `Vector`, funciones que devuelven colecciones,
comparación de cadenas, errores de validación.

```nexis
#inject Vector;
#inject string;

struct Contacto {
    string nombre;
    string telefono;
    string correo;
}

Vector<Contacto> agenda = []

func indice_de(string: nombre) -> int {
    for i in 0 ... agenda.length() {
        if (agenda[i].nombre == nombre) {
            emit -> i
        }
    }
    emit -> -1
}

void agregar(string: nombre, string: telefono, string: correo) -> void {
    if (indice_de(nombre) >= 0) {
        lanzar ErrorValidacion("Contacto duplicado: " + nombre)
    }
    agenda.add(Contacto(nombre, telefono, correo))
}

void eliminar(string: nombre) -> void {
    int i = indice_de(nombre)
    if (i < 0) {
        lanzar ErrorValidacion("No existe: " + nombre)
    }
    agenda.remove(i)
}

func buscar(string: nombre) -> Contacto {
    int i = indice_de(nombre)
    if (i < 0) {
        lanzar ErrorValidacion("No existe: " + nombre)
    }
    emit -> agenda[i]
}

func por_prefijo(string: prefijo) -> Vector<Contacto> {
    Vector<Contacto> encontrados = []
    foreach (Contacto c, agenda) {
        if (string.startsWith(c.nombre, prefijo)) {
            encontrados.add(c)
        }
    }
    emit -> encontrados
}

// --- programa ---
agregar("Ana Torres", "111-111", "ana@mail.com")
agregar("Anabel Ruiz", "222-222", "anabel@mail.com")
agregar("Luis Perez", "333-333", "luis@mail.com")
agregar("Eva Diaz", "444-444", "eva@mail.com")

Console.println("contactos: " + agenda.length())

Contacto c = buscar("Luis Perez")
Console.println(c.nombre + " / " + c.telefono + " / " + c.correo)

Vector<Contacto> anas = por_prefijo("Ana")
Console.println("prefijo Ana: " + anas.length())
foreach (Contacto x, anas) {
    Console.println("- " + x.nombre)
}

eliminar("Eva Diaz")
Console.println("tras eliminar: " + agenda.length())

try {
    agregar("Ana Torres", "999", "otra@mail.com")
} catch (ErrorValidacion e) {
    Console.println("Error: " + e.mensaje())
}

try {
    buscar("Pedro")
} catch (ErrorValidacion e) {
    Console.println("Error: " + e.mensaje())
}
```

Salida:

```
contactos: 4
Luis Perez / 333-333 / luis@mail.com
prefijo Ana: 2
- Ana Torres
- Anabel Ruiz
tras eliminar: 3
Error: Contacto duplicado: Ana Torres
Error: No existe: Pedro
```

> `por_prefijo` devuelve un `Vector<Contacto>` nuevo. Recuerda que devolver una
> colección la copia al llamador, así que puedes modificarla sin afectar la
> agenda original.

---

## 3. Análisis de texto

**Objetivo:** contar palabras, encontrar las más frecuentes, la más larga y
estadísticas básicas.

**Conceptos:** `Map`, `Vector`, `string.split/lowercase/length`, ordenamiento
con desempate, funciones auxiliares.

```nexis
#inject Map;
#inject Vector;
#inject string;

string TEXTO = "nexis es un lenguaje simple y nexis es rapido y simple"

func palabras() -> Vector<string> {
    Vector<string> crudas = string.split(string.lowercase(TEXTO), " ")
    Vector<string> limpias = []
    foreach (p in crudas) {
        if (string.length(p) > 0) {
            limpias.add(p)
        }
    }
    emit -> limpias
}

func frecuencias(Vector<string>: lista) -> Map<string, int> {
    Map<string, int> f = {}
    foreach (p in lista) {
        if (f.contains(p)) {
            f.put(p, f.get(p) + 1)
        } else {
            f.put(p, 1)
        }
    }
    emit -> f
}

func ranking(Map<string, int>: f) -> Vector<string> {
    Vector<string> claves = f.keys()
    for i in 0 ... claves.length() - 1 {
        int mejor = i
        for j in i + 1 ... claves.length() {
            int fj = f.get(claves[j])
            int fm = f.get(claves[mejor])
            if (fj > fm || (fj == fm && claves[j] < claves[mejor])) {
                mejor = j
            }
        }
        if (mejor != i) {
            string tmp = claves[i]
            claves[i] = claves[mejor]
            claves[mejor] = tmp
        }
    }
    emit -> claves
}

func palabra_mas_larga(Vector<string>: lista) -> string {
    string larga = ""
    foreach (p in lista) {
        if (string.length(p) > string.length(larga)) {
            larga = p
        }
    }
    emit -> larga
}

func promedio_longitud(Vector<string>: lista) -> double {
    int total = 0
    foreach (p in lista) {
        total = total + string.length(p)
    }
    emit -> double(total) / double(lista.length())
}

// --- programa ---
Vector<string> lista = palabras()
Map<string, int> f = frecuencias(lista)
Vector<string> top = ranking(f)

Console.println("palabras: " + lista.length())
Console.println("distintas: " + top.length())
Console.println("mas larga: " + palabra_mas_larga(lista))
Console.println("promedio: " + promedio_longitud(lista))

Console.println("top 3:")
for i in 0 ... 3 {
    Console.println((i + 1) + ". " + top[i] + " (" + f.get(top[i]) + ")")
}

Console.println("'nexis' aparece " + f.get("nexis") + " veces")
```

Salida:

```
palabras: 11
distintas: 7
mas larga: lenguaje
promedio: 4
top 3:
1. es (2)
2. nexis (2)
3. simple (2)
'nexis' aparece 2 veces
```

> El desempate alfabético hace que `simple`, `nexis` y `es` salgan siempre en
> el mismo orden aunque tengan la misma frecuencia.

---

## 4. Gestor de tareas con deshacer

**Objetivo:** agregar tareas, procesarlas en orden FIFO, completarlas y
deshacer la última acción.

**Conceptos:** `struct`, `Vector`, `Queue`, `Stack`, funciones que modifican
estado global, validaciones.

```nexis
#inject Vector;
#inject Queue;
#inject Stack;

struct Tarea {
    string titulo;
    int prioridad;
    bool hecha;
}

Vector<Tarea> tareas = []
Queue<int> pendientes = []
Stack<string> historial = []

void agregar(string: titulo, int: prioridad) -> void {
    tareas.add(Tarea(titulo, prioridad, false))
    pendientes.enqueue(tareas.length() - 1)
}

func indice_de(string: titulo) -> int {
    for i in 0 ... tareas.length() {
        if (tareas[i].titulo == titulo) {
            emit -> i
        }
    }
    emit -> -1
}

void completar(string: titulo) -> void {
    int i = indice_de(titulo)
    if (i < 0) {
        lanzar ErrorValidacion("Tarea inexistente: " + titulo)
    }
    Tarea t = tareas[i]
    if (t.hecha) {
        lanzar ErrorValidacion("Ya estaba hecha: " + titulo)
    }
    t.hecha = true
    tareas[i] = t
    historial.push(titulo)
}

void deshacer() -> void {
    if (historial.isEmpty()) {
        lanzar ErrorValidacion("No hay acciones para deshacer")
    }
    string titulo = historial.pop()
    int i = indice_de(titulo)
    Tarea t = tareas[i]
    t.hecha = false
    tareas[i] = t
}

func pendientes_count() -> int {
    int total = 0
    foreach (Tarea t, tareas) {
        if (!t.hecha) {
            total = total + 1
        }
    }
    emit -> total
}

func prioridad_alta() -> Vector<string> {
    Vector<string> lista = []
    foreach (Tarea t, tareas) {
        if (t.prioridad >= 3 && !t.hecha) {
            lista.add(t.titulo)
        }
    }
    emit -> lista
}

// --- programa ---
agregar("Disenar API", 3)
agregar("Escribir tests", 3)
agregar("Actualizar docs", 1)
agregar("Revisar PR", 2)

Console.println("tareas: " + tareas.length())
Console.println("pendientes: " + pendientes_count())

// procesar la cola FIFO
while (!pendientes.isEmpty()) {
    int idx = pendientes.dequeue()
    Console.println("procesando: " + tareas[idx].titulo)
    completar(tareas[idx].titulo)
}

Console.println("pendientes tras procesar: " + pendientes_count())
Console.println("historial: " + historial.length())

deshacer()
Console.println("tras deshacer: " + pendientes_count())
Console.println("ultima hecha: " + tareas[indice_de("Revisar PR")].hecha)

Vector<string> altas = prioridad_alta()
Console.println("prioridad alta pendiente: " + altas.length())
foreach (t in altas) {
    Console.println("- " + t)
}

try {
    completar("Inexistente")
} catch (ErrorValidacion e) {
    Console.println("Error: " + e.mensaje())
}

try {
    deshacer()
    deshacer()
    deshacer()
    deshacer()
    deshacer()
} catch (ErrorValidacion e) {
    Console.println("Error: " + e.mensaje())
}
```

Salida:

```
tareas: 4
pendientes: 4
procesando: Disenar API
procesando: Escribir tests
procesando: Actualizar docs
procesando: Revisar PR
pendientes tras procesar: 0
historial: 4
tras deshacer: 1
ultima hecha: false
prioridad alta pendiente: 0
Error: Tarea inexistente: Inexistente
Error: No hay acciones para deshacer
```

> La `Queue` garantiza el orden de llegada y la `Stack` guarda el historial
> para deshacer en orden inverso (LIFO).

---

## 5. Red de rutas

**Objetivo:** modelar ciudades y conexiones, calcular grados, comprobar
alcanzabilidad y recorrer la red en anchura y profundidad.

**Conceptos:** `Graph`, `Queue`, `Set`, `Map`, `Vector`, recorridos BFS/DFS.

```nexis
#inject Graph;
#inject Queue;
#inject Set;
#inject Map;
#inject Vector;

Graph<string> red = Graph()

void conectar(string: a, string: b, int: km) -> void {
    red.connect(a, b, km)
    red.connect(b, a, km)
}

func grado(string: ciudad) -> int {
    emit -> red.neighbors(ciudad).length()
}

func alcanzables(string: origen) -> Vector<string> {
    Set<string> vistos = {}
    Queue<string> cola = []
    Vector<string> orden = []

    cola.enqueue(origen)
    vistos.add(origen)

    while (!cola.isEmpty()) {
        string actual = cola.dequeue()
        orden.add(actual)
        Vector<string> vecinos = red.neighbors(actual)
        foreach (v in vecinos) {
            if (!vistos.contains(v)) {
                vistos.add(v)
                cola.enqueue(v)
            }
        }
    }

    emit -> orden
}

func distancia_saltos(string: origen, string: destino) -> int {
    Map<string, int> dist = {}
    Queue<string> cola = []

    dist.put(origen, 0)
    cola.enqueue(origen)

    while (!cola.isEmpty()) {
        string actual = cola.dequeue()
        if (actual == destino) {
            emit -> dist.get(actual)
        }
        Vector<string> vecinos = red.neighbors(actual)
        foreach (v in vecinos) {
            if (!dist.contains(v)) {
                dist.put(v, dist.get(actual) + 1)
                cola.enqueue(v)
            }
        }
    }

    emit -> -1
}

// --- programa ---
red.addNode("Lima")
red.addNode("Cusco")
red.addNode("Arequipa")
red.addNode("Trujillo")
red.addNode("Iquitos")

conectar("Lima", "Cusco", 1100)
conectar("Lima", "Arequipa", 1000)
conectar("Arequipa", "Cusco", 500)
conectar("Lima", "Trujillo", 560)

Console.println("ciudades: " + red.length())
Console.println("grado Lima: " + grado("Lima"))
Console.println("grado Iquitos: " + grado("Iquitos"))

Vector<string> alcanzables_desde_lima = alcanzables("Lima")
Console.println("alcanzables: " + alcanzables_desde_lima.length())
foreach (c in alcanzables_desde_lima) {
    Console.println("- " + c)
}

Console.println("Lima -> Cusco: " + distancia_saltos("Lima", "Cusco") + " saltos")
Console.println("Lima -> Trujillo: " + distancia_saltos("Lima", "Trujillo") + " saltos")
Console.println("Lima -> Iquitos: " + distancia_saltos("Lima", "Iquitos") + " saltos")

Console.println("BFS desde Lima:")
red.breadthFirst("Lima")

Console.println("DFS desde Lima:")
red.depthFirst("Lima")

red.disconnect("Lima", "Trujillo")
red.disconnect("Trujillo", "Lima")
Console.println("grado Lima tras cortar: " + grado("Lima"))
Console.println("Trujillo alcanzable: " + (distancia_saltos("Lima", "Trujillo") >= 0))
```

Salida:

```
ciudades: 5
grado Lima: 3
grado Iquitos: 0
alcanzables: 4
- Lima
- Arequipa
- Cusco
- Trujillo
Lima -> Cusco: 1 saltos
Lima -> Trujillo: 1 saltos
Lima -> Iquitos: -1 saltos
BFS desde Lima:
Lima
Arequipa
Cusco
Trujillo
DFS desde Lima:
Lima
Arequipa
Cusco
Trujillo
grado Lima tras cortar: 2
Trujillo alcanzable: false
```

> `Graph` usa un `BTreeMap`, así que `neighbors`, BFS y DFS salen en orden
> alfabético y la salida es reproducible. Las aristas son dirigidas: por eso
> `conectar` llama a `connect` en ambos sentidos.

---

## 6. Cómo organizar un proyecto real

Cuando el programa crece, separa el código en archivos `.nex` y usa
`#inject "archivo.nex";`. La estructura recomendada:

```text
mi-proyecto/
├── main.nxs
├── modelos/
│   ├── producto.nex
│   └── cliente.nex
├── logica/
│   ├── inventario.nex
│   └── ventas.nex
└── datos/
    └── config.nex
```

Cada módulo declara sus propios `#inject`:

```text
# logica/inventario.nex
#inject Vector;
#inject "../modelos/producto.nex";

Vector<Producto> inventario = []

func total() -> int {
    int suma = 0
    foreach (Producto p, inventario) {
        suma = suma + p.precio * p.stock
    }
    emit -> suma
}
```

Y el programa principal importa lo que necesita:

```text
# main.nxs
#inject "logica/inventario.nex";

Console.println(total())
```

> Los módulos propios se resuelven con rutas relativas al archivo que los
> importa. La suite del compilador prueba un ejemplo funcional en
> `compiler/examples/07_modulos/`.

### Lista de comprobación

- [ ] Una responsabilidad por archivo (`modelos`, `logica`, `main`).
- [ ] `#inject` solo de lo que se usa en ese archivo.
- [ ] Errores de negocio con `lanzar ErrorValidacion(...)`.
- [ ] Entradas del usuario validadas antes de operar.
- [ ] Salidas deterministas: ordena claves de `Map`/`Set` antes de imprimir.
- [ ] Casos límite probados: colección vacía, duplicados, valores negativos.
