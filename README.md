# C++ RYCHLÁ REFERENCE / C++ TAHÁK

Vytvořil jsem pro doplnění český překlad komentářů. Jakékoliv další připomínky a návrhy jsou velmi vítány.

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

## Functions - Funkce

```cpp
int f(int x, int y);        // f je funkce přijímající 2 celá čísla a vracející celé číslo
void f();                   // f je procedura bez parametrů
void f(int a=0);            // f() je ekvivalentní f(0)
f();                        // výchozím návratovým typem je celé číslo
inline f();                 // Optimalizace rychlosti
f() { statements; }         // Definice funkce (musí být globální)
T operator+(T x, T y);      // a+b (Jestliže jsou typu T) volají operator+(a, b)
T operator-(T x);           // -a volá funkci operator-(a)
T operator++(int);          // postfix ++ nebo -- (parametr je ignorován)
extern "C" {void f();}      // f() bylo kompilováno v C
```

Parametry funkcí a návratové hodnoty mohou být libovolného typu. Funkce musí být buď deklarovaná,
nebo definovaná dříve, než se začne používat. Může být nejprve deklarovaná a definovaná později.
Každý program se skládá ze sady globálních proměnných deklarací a sady definic funkcí
(mohou být v samostatných souborech), z nichž jedna funkce musí být:

```cpp
int main()  { příkazy... }     // nebo
int main(int argc, char* argv[]) { příkazy... }
```

`argv` je pole řetězců `argc` z příkazové řádky.
Dle konvencí , funkce `main` vrací status `0` jestliže je úspěšná, `1` nebo vyšíí při neúspěchu.

Funkce se stejným jménem mohou mít jiné parametry, pak jsou tzv. přetížené.
Operátory mimo `::` `.` `.*` `?:` mohou být přetížené. Pořadí priority není ovlivněno.
Nelze vytvořit nové operátory.

## Expressions - Výrazy

Operátory jsou seskupeny podle priority, nejvyšší jako první. Unární operátory a přiřazení se vyhodnocují zprava doleva.
Všechna ostatní zleva doprava. Priorita nemá vliv na pořadí hodnocení, které není definované.
Neexistují žádné provozní kontroly pole mimo meze, neplatné ukazatele atd.

```cpp
T::X                        // Název X definovaný ve třídě T
N::X                        // Název X definovaný ve jmenném prostoru N
::X                         // Globalní název X

t.x                         // Člen x struktury nebo třídy t
p->x                        // Člen x struktury nebo třídy ukazující pomocí p
a[n]                        // eNtý prvek pole
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

sizeof x                    // Počet bajtů použitých k reprezentaci objektu x
sizeof(T)                   // Počet bajtů použitých k reprezentaci typu T
++x                         // Přičtení 1 k x, vyhodnocení nové hodnoty (prefix)
--x                         // Odečtení 1 od x, vyhodnocení nové hodnoty
~x                          // Bitový doplněk x
!x                          // Platí (pravda) když x je 0, jinak nepravda (1 nebo 0 v C)
-x                          // Unární mínus
+x                          // Unární plus (výchozí)
&x                          // Adresa x (neboli x je alias)
*p                          // Obsah adresy p (*&x je stejný jako x)
new T                       // Adresa nově alokovaného objektu typu T
new T(x, y)                 // Adresa T inicializovaného s x a y
new T[x]                    // Adresa alokovaného pole prvků T
delete p                    // Zničení a uvolnění objektů na adrese p
delete[] p                  // Zničení a uvolnění pole objektů p
(T) x                       // Konverze x na T (zastaralé, používá se .._cast<T>(x))

x * y                       // Násobení
x / y                       // Dělení (celá čísla zaokrouhlená k 0)
x % y                       // Modulo (výsledek obdrží znaménko od x)

x + y                       // Přičtení, nebo může být posun v poli \&x[y]
x - y                       // Odečtení, nebo počet prvků z *x do *y
x << y                      // posun x o y bitů doleva (x * pow(2, y))
x >> y                      // posun x o y bitů doprava (x / pow(2, y))

x < y                       // Menší než
x <= y                      // Menší než, nebo se rovná
x > y                       // Větší než
x >= y                      // Větší než, nebo se rovná

x & y                       // Bitové AND (3 & 6 je 2)
x ^ y                       // Bitové exklusuvní OR (3 ^ 6 je 5)
x | y                       // Bitové OR (3 | 6 je 7)
x && y                      // x AND pak y (vyhodnocení y jen pokud x (není 0))
x || y                      // x OR jinak y (vyhodnocení y jen když x je nepravda (0))
x = y                       // Přiřazení y k x, vrácení nové hodnoty do x
x += y                      // x = x + y, také -= *= /= <<= >>= &= |= ^=
x ? y : z                   // y když x je pravda (nenulová hodnota), jinak z
throw x                     // Vyvolání vyjímky, přerušení, pokud není zachycena
x , y                       // vyhodnocení x a y, vrací y (zřídka používané)
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
using namespace N;          // Udělání T viditelné bez N:: viz. cout;-)
```

## `memory` (dynamic memory management) - pamět (správa dynamické paměti)

```cpp
#include <memory>           // Vložení hlavičky <memory> (jmenný prostor std)
shared_ptr<int> x;          // Prázdný chytrý sdílený ukazatel shared_ptr na celé číslo na haldě.
                            // Používá referenční počítání pro čištění objektů.
x = make_shared<int>(12);   // Alokace hodnoty 12 na haldě.
shared_ptr<int> y = x;      // Kopírování shared_ptr, implicitně změní počet odkazů na 2.
cout << *y;                 // Dereference y k vytištění '12'
if (y.get() == x.get()) {   // Vrácení klasického ukazatele (zde x == y)
    cout << "Stejné";  
}  
y.reset();                  // Eliminuje vlastníka jednoho objektu
if (y.get() != x.get()) { 
    cout << "Rozdílné";  
}  
if (y == nullptr) {         // Porovnávání s nullptr je možné (vracející pravdu)
    cout << "Prázdné";  
}  
y = make_shared<int>(15);   // Přířazení nové hodnoty
cout << *y;                 // Dereference x k vytištění '15'
cout << *x;                 // Dereference x k vytištění '12'
weak_ptr<int> w;            // Vytvoření prázdného slabého ukazatele
w = y;                      // w má slabou referenci na y.
if (shared_ptr<int> s = w.lock()) { // Má být skopírovaný do shared_ptr před použitím
    cout << *s;
}
unique_ptr<int> z;          // Vytvoření prázdného unikátního ukazatele
unique_ptr<int> q;
z = make_unique<int>(16);   // Alokace celého čísla (16) na haldě. Povolená je jen jedna reference.
q = move(z);                // Přesun reference ze z na q.
if (z == nullptr){
    cout << "Z null";
}
cout << *q;
shared_ptr<B> r;
r = dynamic_pointer_cast<B>(t); // Konverze t na shared_ptr<B>

```

## `math.h`, `cmath` (floating point math) - matematika s plovoucí desetinnou čárkou

```cpp
#include <cmath>            // Hlavička cmath (jmenný prostor std)
sin(x); cos(x); tan(x);     // Trigonometrické funkce, x (double) jsou v radiánech
asin(x); acos(x); atan(x);  // Inverze
atan2(y, x);                // atan(y/x)
sinh(x); cosh(x); tanh(x);  // Hyperbolické sin, cos, tan
exp(x); log(x); log10(x);   // e na x, log báze e, log báze 10
pow(x, y); sqrt(x);         // x na y, odmocnina
ceil(x); floor(x);          // Zaokrouhlení nahoru, dolů (jako double)
fabs(x); fmod(x, y);        // Absolutní hodnota, x modulo y
```

## `assert.h`, `cassert` (Debugging Aid) - Debugovací první pomoc

```cpp
#include <cassert>        // Hlavička iostream (jmenný prostor std)
assert(e);                // Jestliže e je nepravda, následuje vytisknutí zprávy a ukončení
#define NDEBUG            // (před #include <assert.h>), vypnutí assert
```

## `iostream.h`, `iostream` (Replaces `stdio.h`) - iostream nahrazuje stdio.h

```cpp
#include <iostream>         // Hlavička iostream (jmenný prostor std)
cin >> x >> y;              // Čtení slov x a y (jakéhokoliv typu) z proudu stdin
cout << "x=" << 3 << endl;  // Vypsání řádky do proudu stdout
cerr << x << y << flush;    // Vypsání do proudu stderr a vyčištění
c = cin.get();              // c = getchar();
cin.get(c);                 // Čtení znaku
cin.getline(s, n, '\n');    // Čtení řádky do typu char s[n] do konce řádku '\n' (výchozí)
if (cin)                    // Dobrý stav (nikoliv EOF)?
                            // Ke čtení/zápisu libovolného typu T:
istream& operator>>(istream& i, T& x) {i >> ...; x=...; vrácení i;}
ostream& operator<<(ostream& o, const T& x) {vrácení o << ...;}
```

## `fstream.h`, `fstream` (File I/O works like `cin`, `cout` as above) - pracuje stejně jako cin, cout zmíněný výše


```cpp
#include <fstream>          // Hlavička filestream (jmenný prostor std)
ifstream f1("filename");    // Otevření textového souboru pro čtení
if (f1)                     // Test otevření a možnosti vstupu
    f1 >> x;                // Čtení objektu ze souboru
f1.get(s);                  // Čtení znaku, nebo řádky
f1.getline(s, n);           // Čtení řádky do řetězce (string s[n])
ofstream f2("filename");    // Otevření souboru pro zápis
if (f2) f2 << x;            // Zápis do souboru
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

## `thread` (Multi-threading library) - Více-vláknová knihovna
```cpp
#include <thread>         // Hlavička thread
                          // Hardware vlákna (nebo 0 pro neznámé)
unsigned c = std::thread::hardware_concurrency();
auto lambdaFn = []() {    // Lambda funkce použitá pro tělo vlákna
    cout << "Ahoj vícevláknově";
};
thread t(lambdaFn);       // Vytvoření a spuštění vlákna pomocí lambda funkce
t.join();                 // Čekání hlavního vlákna na dokončení vlákna t

// --- shared resource example --- // --- příklady sdílených zdrojů ---
mutex mut;                // Mutex pro synchronizaci
condition_variable cond;  // Sdílená podmíněná proměnná
const char *sharedMes     // Sdílený zdroj
    = nullptr;
auto pingPongFn =         // Tělo vlákna (lambda funkce). Tisk zprávy někoho jiného
    [&](const char *mes)
{
    while (true)
    {
        unique_lock<mutex> lock(mut);   // Uzamknutí mutexu
        do
        {
            cond.wait(lock, [&]() {     // Čekání na výsledek pravda podmíněné proměnné
                                        // [&] přístup k proměnným z okolí (z vnějšího kontextu)
                                        // Odemknutí v průběhu čekání což umožní ostatním vláknům modifikování
                return sharedMes != mes;// Čekáme na změnu sharedMes, která není stejná jako mes.
            });
        } while (sharedMes == mes);     // Zabraňuje falešnému probuzení
        cout << sharedMes << endl;
        sharedMes = mes;
        lock.unlock();                  // Již není třeba mít zamčeno
        cond.notify_all();              // Probudit všechna vlákna a upozornit na změnu podmínek
    }
};
sharedMes = "ping";
thread t1(pingPongFn, sharedMes);       // Zahájení příkladu s třemi konkurenčními vlákny
thread t2(pingPongFn, "pong");
thread t3(pingPongFn, "boing");
```

## `future` (thread support library) - `future` (knihovna pro podporu vláken)
```cpp
#include <future>         // Hlavička future
function<int(int)> fib =  // Vytvoření lambda funkce
  [&](int i){
    if (i <= 1){
      return 1;
    }
    return fib(i-1) 
         + fib(i-2);
  };
future<int> fut =         // Výsledek asynchronní funkce
  async(launch::async, fib, 4); // Zahájení asynchronní funkce v dalším vlákně
// vykonej nějakou práci
cout << fut.get();        // Získání výsledku z asynchronní funkce. Vyčkávání pokud je potřebné.
```

Překlad a doplnění některých dalších významů - Tomáš Mark (c) 2024
