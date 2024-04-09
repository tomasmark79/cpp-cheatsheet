# C++ RYCHLÁ REFERENCE / C++ TAHÁK

Český překlad komentářů Tomáš Mark.
Dokument je k dispozici v repositáři na https://github.com/tomasmark79/cpp-cheatsheet.
Jakékoliv další připomínky a návrhy jsou velmi vítány. Původní zdroj v angličtině najdete v popisu u forku.

## Preprocessor - Preprocesor

```cpp
                            // Komentář do konce řádku
                            /* Víceřádkový komentář */
#include  <stdio.h>         // Vložení standardního hlavičkového souboru
#include "myfile.h"         // Vložení s. h. souboru v akt. pracovní složce
#define X jsem text         // Nahradí X textem jsem text
#define F(a,b) a+b          // Nahradí F(1,2) s 1+2
#define X \
 jsem text                  // Víceřádková definice
#undef X                    // Zrušení definice
#if defined(X)              // Podmíněná kompilace (#ifdef X)
#else                       // Volitelné (#ifndef X nebo #if !defined(X))
#endif                      // Je vyžadováno po #if, #ifdef
```

## Literals - Literály

```cpp
255, 0377, 0xff             // Celá čísla (decimal, octal, hex)
2147483647L, 0x7fffffffl    // Long (32-bit) celá čísla
123.0, 1.23e2               // Double (reálná) čísla
'a', '\141', '\x61'         // Znak (literál, octal, hex)
'\n', '\\', '\'', '\"'      // Nová řádka, zpětné lomítko, jednoduchá uvozovka, dvojtá uvozovka
"string\n"                  // Pole znaků zakončené novou řádkou a \0
"hello" "world"             // Zřetězené řetězce
true, false                 // Boolova konstanta 1 a 0
nullptr                     // Typ ukazatele s adresou 0
```

## Declarations - Deklarace

```cpp
int x;                      // Deklarace x jako celé číslo (nedefinovaná hodnota)
int x=255;                  // Deklarace a inicializace x na hodnotu 255
short s; long l;            // Obvykle 16 nebo 32 bitové celé číslo(int může být obojí)
char c='a';                 // Obvykle 8 bitový znak
unsigned char u=255;
signed char s=-1;           // typ char umí i signed
unsigned long x =
  0xffffffffL;              // typy short, int, long jsou podepsané (signed)
float f; double d;          // Jednoduchá, dvojitá přesnost reálných čísel (nikdy nějsou nepodepsané)
bool b=true;                // true nebo false, může použít i typ int (1 nebo 0)
int a, b, c;                // Více deklarací
int a[10];                  // Pole s 10 prvky typu int (a[0] až a[9])
int a[]={0,1,2};            // Inicializované pole (nebo a[3]={0,1,2}; )
int a[2][2]={{1,2},{4,5}};  // Pole polí typu int (dvourozměrné pole)
char s[]="hello";           // Řetězec (6 prvků s '\0' na konci)
std::string s = "Hello"     // Vytváří objekt std::string s hodnotou "Hello"
std::string s = R"(Hello
World)";                    // Vytváří objekt std::string s hodnotou "Hello\nWorld"
int* p;                     // p je ukazatel na (adresu v paměti) typu int
char* s="hello";            // s ukazuje na bezejmenné pole obsahující "hello"
void* p=nullptr;            // Adresa paměti bez definovaného typu (nullptr je 0)
int& r=x;                   // r je reference na (alias) int x
enum weekend {SAT,SUN};     // weekend je typ s hodnotami SAT and SUN
enum weekend day;           // day je proměnná typu weekend
enum weekend{SAT=0,SUN=1};  // Explicitní reprezentace jako typ int
enum {SAT,SUN} day;         // Anonymní enum
enum class Color {Red,Blue};// Color je striktní typ s hodnotami Red a Blue
Color x = Color::Red;       // Přiřazení Color x k red
typedef String char*;       // String s; znamená char* s;
const int c=3;              // Konstanty musí být inicializované, nelze jim přiřazovat
const int* p=a;             // Obsah p (prvky a) jsou konstanty
int* const p=a;             // p (nikoliv obsah) jsou konstanty
const int* const p=a;       // Obojí p i jeho obsah jsou konstanty
const int& cr=x;            // cr nemůže přiřadit změnu pro x
int8_t,uint8_t,int16_t,
uint16_t,int32_t,uint32_t,
int64_t,uint64_t            // Standardní typy pevné délky
auto it = m.begin();        // Deklarace it dle výsledku m.begin()
auto const param = config["param"];
                            // Deklarace it dle výsledku jako konstanta
auto& s = singleton::instance();
                            // Deklarace s dle výsledku jako reference
```

## STORAGE Classes - Úložné třídy

```cpp
int x;                      // Auto (pamět existuje pouze uvnitř pole působnosti)
static int x;               // Globální životnost i když je deklarována v místním rozsahu
extern int x;               // Pouze informace, deklarované v jiném prostoru
```

## Statements - Příkazy

```cpp
x=y;                        // Každý výraz je příkazem
int x;                      // Deklarace je příkaz
;                           // Prázdný příkaz
{                           // Blok je jednoduchý příkaz
    int x;                  // Rozsah x je deklarován do konce bloku
}
if (x) a;                   // Jestliže x je pravda (není 0), vyhodnoť a
else if (y) b;              // Jestliže není x a y (volitelné, lze opakovat)
else c;                     // Jestliže není x a není y (volitelné)

while (x) a;                // Vejdi a opakuj pouze pokud x je pravda
                            (pokud x není 0)

for (x; y; z) a;            // Ekvivalent k: x; while(y) {a; z;}

for (x : y) a;              // Cyklus na bázy rozsahu, např.
                            // Pro (auto& x v seznamu) x.y();

do a; while (x);            // Ekvivalent k: a; while(x) a;

switch (x) {                // x musí být celé číslo (int)
    case X1: a;             // Pokud x == X1 (musí být konstanta), skoč sem
    case X2: b;             // Jinak když x == X2, skoč sem
    default: c;             // Jinak skoč sem (volitelná klauzule)
}
break;                      // Vyskoč z cyklů jako while, do, for, nebo switch
continue;                   // Skoč na začátek cyklů jako while, do, nebo for
return x;                   // Vrať x z funkce k volanému
try { a; }
catch (T t) { b; }          // Při vyjímce T skoč sem
catch (...) { c; }          // Při jakékéliv vyjímce skoč sem
```

## Functions

```cpp
int f(int x, int y);        // f is a function taking 2 ints and returning int
void f();                   // f is a procedure taking no arguments
void f(int a=0);            // f() is equivalent to f(0)
f();                        // Default return type is int
inline f();                 // Optimize for speed
f() { statements; }         // Function definition (must be global)
T operator+(T x, T y);      // a+b (if type T) calls operator+(a, b)
T operator-(T x);           // -a calls function operator-(a)
T operator++(int);          // postfix ++ or -- (parameter ignored)
extern "C" {void f();}      // f() was compiled in C
```

Function parameters and return values may be of any type. A function must either be declared or defined before
it is used. It may be declared first and defined later. Every program consists of a set of a set of global variable
declarations and a set of function definitions (possibly in separate files), one of which must be:

```cpp
int main()  { statements... }     // or
int main(int argc, char* argv[]) { statements... }
```

`argv` is an array of `argc` strings from the command line.
By convention, `main` returns status `0` if successful, `1` or higher for errors.

Functions with different parameters may have the same name (overloading). Operators except `::` `.` `.*` `?:` may be overloaded.
Precedence order is not affected. New operators may not be created.

## Expressions

Operators are grouped by precedence, highest first. Unary operators and assignment evaluate right to left. All
others are left to right. Precedence does not affect order of evaluation, which is undefined. There are no run time
checks for arrays out of bounds, invalid pointers, etc.

```cpp
T::X                        // Název X definován ve třídě T
N::X                        // Název X definován ve jmenném prostoru N
::X                         // Globalní název X

t.x                         // Člen x struktury nebo třídy t
p->x                        // Člen x struktury nebo třídy ukazující pomocí p
a[n]                        // eNtý element pole
f(x,y)                      // Volání funkce f s argumenty x and y
T(x,y)                      // Objekt třídy T inicializovaný x a y
x++                         // Přičtení 1 do x, vyhodnotí se jako původní x (postfix)
x--                         // Odečtení 1 od x, vyhodnotí se jako původní x
typeid(x)                   // Typ x
typeid(T)                   // Stejné jako typeid(x) pokud x je T
dynamic_cast< T>(x)         // Převádí x na T s kontrolou za běhu
static_cast< T>(x)          // Převádí x na T, bez kontroly
reinterpret_cast< T>(x)     // interpretuje bity x jako T
const_cast< T>(x)           // Převádí x na stejný typ T jen odebere modifikátor const

sizeof x                    // Number of bytes used to represent object x
sizeof(T)                   // Number of bytes to represent type T
++x                         // Add 1 to x, evaluates to new value (prefix)
--x                         // Subtract 1 from x, evaluates to new value
~x                          // Bitwise complement of x
!x                          // true if x is 0, else false (1 or 0 in C)
-x                          // Unary minus
+x                          // Unary plus (default)
&x                          // Address of x
*p                          // Contents of address p (*&x equals x)
new T                       // Address of newly allocated T object
new T(x, y)                 // Address of a T initialized with x, y
new T[x]                    // Address of allocated n-element array of T
delete p                    // Destroy and free object at address p
delete[] p                  // Destroy and free array of objects at p
(T) x                       // Convert x to T (obsolete, use .._cast<T>(x))

x * y                       // Multiply
x / y                       // Divide (integers round toward 0)
x % y                       // Modulo (result has sign of x)

x + y                       // Add, or \&x[y]
x - y                       // Subtract, or number of elements from *x to *y
x << y                      // x shifted y bits to left (x * pow(2, y))
x >> y                      // x shifted y bits to right (x / pow(2, y))

x < y                       // Less than
x <= y                      // Less than or equal to
x > y                       // Greater than
x >= y                      // Greater than or equal to

x & y                       // Bitwise and (3 & 6 is 2)
x ^ y                       // Bitwise exclusive or (3 ^ 6 is 5)
x | y                       // Bitwise or (3 | 6 is 7)
x && y                      // x and then y (evaluates y only if x (not 0))
x || y                      // x or else y (evaluates y only if x is false (0))
x = y                       // Assign y to x, returns new value of x
x += y                      // x = x + y, also -= *= /= <<= >>= &= |= ^=
x ? y : z                   // y if x is true (nonzero), else z
throw x                     // Throw exception, aborts if not caught
x , y                       // evaluates x and y, returns y (seldom used)
```

## Classes - Třídy

```cpp
class T {                   // Nový typ
private:                    // Sekce přístupná jen pro metody T
protected:                  // Sekce přístupná také pro zděděné třídy z T
public:                     // Přístupná všem
    int x;                  // Datová složka třídy
    void f();               // Metoda třídy
    void g() {return;}      // Vložená implementace metody
    void h() const;         // Neovlivňuje datové složky třídy
    int operator+(int y);   // t+y představuje t.operator+(y)
    int operator-();        // -t se představuje t.operator-()
    T(): x(1) {}            // Konstruktor se seznamem inicializace
    T(const T& t): x(t.x) {}// Kopírovací konstruktor
    T& operator=(const T& t)
    {x=t.x; return *this; } // Přiřazovací operátor
    ~T();                   // Destruktor (automatická čistící funkce)
    explicit T(int a);      // Umožňuje t=T(3) ale ne t=3
    T(float x): T((int)x) {}// Delegovaný konstruktor na T(int)
    operator int() const
    {return x;}             // Umožnuje int(t)
    friend void i();        // Globální funkce i() se soukromým přístupem
    friend class U;         // Členové třídy U se soukromým přístupem
    static int y;           // Sdílená proměnná mezi všemi objekty T
    static void l();        // Sdílený kód. y může přistupovat, ale ne x
    class Z {};             // Vnořená třída T::Z
    typedef int V;          // T::V představuje typ int
};
void T::f() {               // Kód pro členskou funkci f třídy T
    this->x = x;}           // toto je adresa sebe sama (představuje x=x;)
int T::y = 2;               // Inicializace statické proměnné (vyžadováno)
T::l();                     // Volání statické metody
T t;                        // Vytvoří objekt s implicitním voláním konstruktoru
t.f();                      // Volá metodu f na objektu T

struct T {                  // Stejné jako: class T { public:
  virtual void i();         // Může být přepsán za běhu zděděnou třídou
  virtual void g()=0; };    // Musí být přepsán za běhu zděděnou třídou (čistě abstraktní)
class U: public T {         // Zděděná třída U dědí všechny členy třídy předka T
  public:
  void g(int) override; };  // Přepsání metody g
class V: private T {};      // Zděděné členy třídy T se stávají private
class W: public T, public U {};
                            // Vícenásobná dědičnost
class X: public virtual T {};
                            // Třídy zděděné ze třídy X mají stejného předka třídy T
```

Všechny třídy mají výchozí kopírovací konstruktor, přiřazovací operátor a destruktor, které provádějí související operace na každém datové složce a na každé rodičovské třídě, tak jak je uvedeno výše. K dispozici je také výchozí konstruktor bez argumentů (vyžadován k vytvoření polí), pokud třída nemá žádný konstruktor. Konstruktory, přiřazení a destruktory nedědí.

## Templates - Šablony

```cpp
template <class T> T f(T t);// Přetíží funkci f pro všechny typy
template <class T> class X {// Třída s <parametrem> typu T 
  X(T t); };                // a konstruktorem
template <class T> X<T>::X(T t) {}
                            // Definice konstruktoru
X<int> x(3);                // Vytvoří objekt x třídy X typu <int>
template <class T, class U=T, int n=0>
                            // Třída s implicitním 2. a 3. parametrem
```

## Namespaces - Jmenné prostory

```cpp
namespace N {class T {};}   // Zakrytí T v prostoru N
N::T t;                     // Použití jména T v prostoru N
using namespace N;          // Udělej T viditelné bez N:: viz. cout;-)
```

## `memory` (dynamic memory management)

```cpp
#include <memory>           // Include memory (std namespace)
shared_ptr<int> x;          // Empty shared_ptr to a integer on heap. Uses reference counting for cleaning up objects.
x = make_shared<int>(12);   // Allocate value 12 on heap
shared_ptr<int> y = x;      // Copy shared_ptr, implicit changes reference count to 2.
cout << *y;                 // Dereference y to print '12'
if (y.get() == x.get()) {   // Raw pointers (here x == y)
    cout << "Same";  
}  
y.reset();                  // Eliminate one owner of object
if (y.get() != x.get()) { 
    cout << "Different";  
}  
if (y == nullptr) {         // Can compare against nullptr (here returns true)
    cout << "Empty";  
}  
y = make_shared<int>(15);   // Assign new value
cout << *y;                 // Dereference x to print '15'
cout << *x;                 // Dereference x to print '12'
weak_ptr<int> w;            // Create empty weak pointer
w = y;                      // w has weak reference to y.
if (shared_ptr<int> s = w.lock()) { // Has to be copied into a shared_ptr before usage
    cout << *s;
}
unique_ptr<int> z;          // Create empty unique pointers
unique_ptr<int> q;
z = make_unique<int>(16);   // Allocate int (16) on heap. Only one reference allowed.
q = move(z);                // Move reference from z to q.
if (z == nullptr){
    cout << "Z null";
}
cout << *q;
shared_ptr<B> r;
r = dynamic_pointer_cast<B>(t); // Converts t to a shared_ptr<B>

```

## `math.h`, `cmath` (floating point math)

```cpp
#include <cmath>            // Include cmath (std namespace)
sin(x); cos(x); tan(x);     // Trig functions, x (double) is in radians
asin(x); acos(x); atan(x);  // Inverses
atan2(y, x);                // atan(y/x)
sinh(x); cosh(x); tanh(x);  // Hyperbolic sin, cos, tan functions
exp(x); log(x); log10(x);   // e to the x, log base e, log base 10
pow(x, y); sqrt(x);         // x to the y, square root
ceil(x); floor(x);          // Round up or down (as a double)
fabs(x); fmod(x, y);        // Absolute value, x mod y
```

## `assert.h`, `cassert` (Debugging Aid)

```cpp
#include <cassert>        // Include iostream (std namespace)
assert(e);                // If e is false, print message and abort
#define NDEBUG            // (before #include <assert.h>), turn off assert
```

## `iostream.h`, `iostream` (Replaces `stdio.h`)

```cpp
#include <iostream>         // Include iostream (std namespace)
cin >> x >> y;              // Read words x and y (any type) from stdin
cout << "x=" << 3 << endl;  // Write line to stdout
cerr << x << y << flush;    // Write to stderr and flush
c = cin.get();              // c = getchar();
cin.get(c);                 // Read char
cin.getline(s, n, '\n');    // Read line into char s[n] to '\n' (default)
if (cin)                    // Good state (not EOF)?
                            // To read/write any type T:
istream& operator>>(istream& i, T& x) {i >> ...; x=...; return i;}
ostream& operator<<(ostream& o, const T& x) {return o << ...;}
```

## `fstream.h`, `fstream` (File I/O works like `cin`, `cout` as above)


```cpp
#include <fstream>          // Include filestream (std namespace)
ifstream f1("filename");    // Open text file for reading
if (f1)                     // Test if open and input available
    f1 >> x;                // Read object from file
f1.get(s);                  // Read char or line
f1.getline(s, n);           // Read line into string s[n]
ofstream f2("filename");    // Open file for writing
if (f2) f2 << x;            // Write to file
```

## `string` (Variable sized character array)

```cpp
#include <string>         // Include string (std namespace)
string s1, s2="hello";    // Create strings
s1.size(), s2.size();     // Number of characters: 0, 5
s1 += s2 + ' ' + "world"; // Concatenation
s1 == "hello world"       // Comparison, also <, >, !=, etc.
s1[0];                    // 'h'
s1.substr(m, n);          // Substring of size n starting at s1[m]
s1.c_str();               // Convert to const char*
s1 = to_string(12.05);    // Converts number to string
getline(cin, s);          // Read line ending in '\n'
```

## `vector` (Variable sized array/stack with built in memory allocation)

```cpp
#include <vector>         // Include vector (std namespace)
vector<int> a(10);        // a[0]..a[9] are int (default size is 0)
vector<int> b{1,2,3};        // Create vector with values 1,2,3
a.size();                 // Number of elements (10)
a.push_back(3);           // Increase size to 11, a[10]=3
a.back()=4;               // a[10]=4;
a.pop_back();             // Decrease size by 1
a.front();                // a[0];
a[20]=1;                  // Crash: not bounds checked
a.at(20)=1;               // Like a[20] but throws out_of_range()
for (int& p : a)
  p=0;                    // C++11: Set all elements of a to 0
for (vector<int>::iterator p=a.begin(); p!=a.end(); ++p)
  *p=0;                   // C++03: Set all elements of a to 0
vector<int> b(a.begin(), a.end());  // b is copy of a
vector<T> c(n, x);        // c[0]..c[n-1] init to x
T d[10]; vector<T> e(d, d+10);      // e is initialized from d
```

## `deque` (Array stack queue)

`deque<T>` is like `vector<T>`, but also supports:

```cpp
#include <deque>          // Include deque (std namespace)
a.push_front(x);          // Puts x at a[0], shifts elements toward back
a.pop_front();            // Removes a[0], shifts toward front
```

## `utility` (pair)

```cpp
#include <utility>        // Include utility (std namespace)
pair<string, int> a("hello", 3);  // A 2-element struct
a.first;                  // "hello"
a.second;                 // 3
```

## `map` (associative array - usually implemented as binary search trees - avg. time complexity: O(log n))

```cpp
#include <map>            // Include map (std namespace)
map<string, int> a;       // Map from string to int
a["hello"] = 3;           // Add or replace element a["hello"]
for (auto& p:a)
    cout << p.first << p.second;  // Prints hello, 3
a.size();                 // 1
```

## `unordered_map` (associative array - usually implemented as hash table - avg. time complexity: O(1))

```cpp
#include <unordered_map>  // Include map (std namespace)
unordered_map<string, int> a; // Map from string to int
a["hello"] = 3;           // Add or replace element a["hello"]
for (auto& p:a)
    cout << p.first << p.second;  // Prints hello, 3
a.size();                 // 1
```

## `set` (store unique elements - usually implemented as binary search trees - avg. time complexity: O(log n))

```cpp
#include <set>            // Include set (std namespace)
set<int> s;               // Set of integers
s.insert(123);            // Add element to set
if (s.find(123) != s.end()) // Search for an element
    s.erase(123);
cout << s.size();         // Number of elements in set
```

## `unordered_set` (store unique elements - usually implemented as a hash set - avg. time complexity: O(1))

```cpp
#include <unordered_set>  // Include set (std namespace)
unordered_set<int> s;     // Set of integers
s.insert(123);            // Add element to set
if (s.find(123) != s.end()) // Search for an element
    s.erase(123);
cout << s.size();         // Number of elements in set
```

## `algorithm` (A collection of 60 algorithms on sequences with iterators)

```cpp
#include <algorithm>      // Include algorithm (std namespace)
min(x, y); max(x, y);     // Smaller/larger of x, y (any type defining <)
swap(x, y);               // Exchange values of variables x and y
sort(a, a+n);             // Sort array a[0]..a[n-1] by <
sort(a.begin(), a.end()); // Sort vector or deque
reverse(a.begin(), a.end()); // Reverse vector or deque
```

## `chrono` (Time related library)
```cpp
#include <chrono>         // Include chrono
using namespace std::chrono; // Use namespace
auto from =               // Get current time_point
  high_resolution_clock::now();
// ... do some work       
auto to =                 // Get current time_point
  high_resolution_clock::now();
using ms =                // Define ms as floating point duration
  duration<float, milliseconds::period>;
                          // Compute duration in milliseconds
cout << duration_cast<ms>(to - from)
  .count() << "ms";
```

## `thread` (Multi-threading library)
```cpp
#include <thread>         // Include thread
unsigned c = 
  hardware_concurrency(); // Hardware threads (or 0 for unknown)
auto lambdaFn = [](){     // Lambda function used for thread body
    cout << "Hello multithreading";
};
thread t(lambdaFn);       // Create and run thread with lambda
t.join();                 // Wait for t finishes

// --- shared resource example ---
mutex mut;                         // Mutex for synchronization
condition_variable cond;           // Shared condition variable
const char* sharedMes              // Shared resource
  = nullptr;
auto pingPongFn =                  // thread body (lambda). Print someone else's message
  [&](const char* mes){
    while (true){
      unique_lock<mutex> lock(mut);// locks the mutex 
      do {                
        cond.wait(lock, [&](){     // wait for condition to be true (unlocks while waiting which allows other threads to modify)        
          return sharedMes != mes; // statement for when to continue
        });
      } while (sharedMes == mes);  // prevents spurious wakeup
      cout << sharedMes << endl;
      sharedMes = mes;       
      lock.unlock();               // no need to have lock on notify 
      cond.notify_all();           // notify all condition has changed
    }
  };
sharedMes = "ping";
thread t1(pingPongFn, sharedMes);  // start example with 3 concurrent threads
thread t2(pingPongFn, "pong");
thread t3(pingPongFn, "boing");
```

## `future` (thread support library)
```cpp
#include <future>         // Include future
function<int(int)> fib =  // Create lambda function
  [&](int i){
    if (i <= 1){
      return 1;
    }
    return fib(i-1) 
         + fib(i-2);
  };
future<int> fut =         // result of async function
  async(launch::async, fib, 4); // start async function in other thread
// do some other work 
cout << fut.get();        // get result of async function. Wait if needed.
```
