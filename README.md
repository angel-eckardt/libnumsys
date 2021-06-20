# libnumsys
Number system conversion library made in C.

## Reasoning
In many applications of computer science, it is necessary to differentiate between the different number systems that programmers use on a day-to-day basis. The most common of these include binary, octal, and hexadecimal. Although one can simply practice conversion between them and regular decimal, such a feat is simply not practical for everyone who needs to use these representations

In other fields, such as in the study of historical number systems, there is also a need for a quick and easy-to-use conversion method. Although impractical to represent all symbols of each system in a single method, numeral systems such as the Sumerian, Babylonian, Mayan, Muisca, and Kaktovik all can have their digits represented in English using the beginning letters of the alphabet, similar to in hexadecimal.

Because of the need for a fast and convenient number system converter, I created this library.

## Usage Notes
At a glance, the library's features include:
```C++
// Negative number representation type
typedef enum {
    NEG_SIGN   = 1, // Append negative sign to front
    SIGN_PLACE = 2, // Append nonzero digit to front
    ONES_COMPL = 4, // Set as complement of positive
    TWOS_COMPL = 8  // Set as complement of positive plus 1
} numrep_t;

// Number system type
typedef struct {
    unsigned base;
    numrep_t rep;
} numsys_t;

// Converts string in given base/representation to integer
long long numsys_tonum(const char *, numsys_t);
unsigned long long numsys_utonum(const char *, unsigned);   // Unsigned ver.

// Converts string in one base/representation to string in another
char *numsys_conv(const char *, numsys_t, numsys_t);
char *numsys_uconv(const char *, unsigned, unsigned);

// Converts integer to string in given base/representation
char *numsys_tostring(long long, numsys_t);
char *numsys_utostring(unsigned long long, unsigned);

// C++ function aliases
namespace numsys {
    long long tonum(const char *, numsys_t);
    unsigned long long utonum(const char *, unsigned);
    char *conv(const char *, numsys_t, numsys_t);
    char *uconv(const char *, unsigned, unsigned);
    char *tostring(long long, numsys_t);
    char *utostring(unsigned long long, unsigned);
}
```
The library contains a single header, `numsys.h`, from which further information can found.

If using the library with stanrd C99 or later, it is useful to know that arguments of type `numsys_t` can be passed without the use of a temporary buffer by using a [compound literal](https://en.cppreference.com/w/c/language/compound_literal). Underscores are allowed in number strings, and are encouraged to preserve readability.
```C
numsys_tonum("1_028", (numsys_t){10, NEG_SIGN});
```
Similarly, in C++, arguments of type `numsys_t` can be passed using an [initializer list](https://en.cppreference.com/w/cpp/utility/initializer_list), as `numsys_t` is considered a [POD type](https://stackoverflow.com/questions/146452/what-are-pod-types-in-c).
```C++
numsys_tostring(0b101101, {2, SIGN_PLACE});
```
