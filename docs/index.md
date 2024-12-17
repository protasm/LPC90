---
layout: default
title: DRAFT LPC90 Language Specification
---

# DRAFT LPC90 Language Specification

<h2 id="toc">Table of Contents</h2>

1. **Introduction**<a id="ch1"></a>  
  1.1 [Purpose of this Specification](#1.1)  
  1.2 [History of LPC](#1.2)  
  1.3 [Design Philosophy](#1.3)  

2. **Lexical Structure**<a id="ch2"></a>  
  2.1 [Characters](#2.1)  
  2.2 [Tokens](#2.2)  
  2.3 [Keywords](#2.3)  
  2.4 [Identifiers](#2.4)  
  2.5 [Literals](#2.5)  
  2.6 [Comments](#2.6)  

3. **Types**<a id="ch3"></a>  
  3.1 [Primitive Types](#3.1)  
  3.2 [Object Types](#3.2)  
  3.3 [Special Types](#3.3) (`nil`, `mixed`)  
  3.4 [Type Conversion](#3.4)  

4. **Variables**<a id="ch4"></a>  
  4.1 [Variable Declarations](#4.1)  
  4.2 [Scope and Lifetime of Variables](#4.1)  
  4.3 [Default Values](#4.1)  

5. **Operators**<a id="ch5"></a>  
  5.1 [Operator Precedence and Associativity](#5.1)  
  5.2 [Arithmetic Operators](#5.2)  
  5.3 [Relational and Logical Operators](#5.3)  
  5.4 [Assignment Operators](#5.4)  

6. **Expressions**<a id="ch6"></a>  
  6.1 [Evaluation Order](#6.1)  
  6.2 [Method Calls](#6.2)  
  6.3 [Field Access](#6.3)  
  6.4 [Conditional Expressions](#6.4)  

7. **Statements**<a id="ch7"></a>  
  7.1 [Block Statements](#7.1)  
  7.2 [Control Flow Statements](#7.2) (`if`, `else`, `while`, `for`)  
  7.3 [Return Statements](#7.3)  

8. **Objects**<a id="ch8"></a>  
  8.1 [Object Definition and Structure](#8.1)  
  8.2 [Fields](#8.2)  
  8.3 [Methods](#8.3)  
  8.4 [Inheritance](#8.4)  

9. **Execution**<a id="ch9"></a>  
  9.1 [Program Entry Point](#9.1)  
  9.2 [Object Instantiation and Initialization](#9.2)  

10. **Preprocessing Directives**<a id="ch10"></a>  
  10.1 [`#include` Directives](#10.1)  
  10.2 [`#define` Macros](#10.2)  

11. **Error Handling**<a id="ch11"></a>  
  11.1 [Syntax Errors](#11.1)  
  11.2 [Runtime Errors](#11.2)  

12. **Appendices**<a id="appendices"></a>  
  A. [Backus-Naur Form (BNF) Grammar](#app-a)  
  B. [Reserved Words](#app-b)  

## 1. Introduction

<h3 id="1.1">1.1 Purpose of this Specification <a href="#ch1">[toc]</a></h3>

The purpose of this specification is to define the syntax, semantics, and structure of LPC, a programming language designed for building and enhancing LPMuds (online, multi-user, text-only role-playing games) &mdash; specifically, as the language existed very soon after its inception. By offering a formal and detailed description of LPC circa 1990, the LPC90 language specification aims to:

1. **Establish a Foundation**: Establish a consistent and widely accepted foundation that describes an original (or near-original) dialect of LPC, providing a common starting point from which future LPC specifications can evolve;

2. **Facilitate Compatibility**: Provide a clear and consistent reference for developers working with or adapting legacy LPC-based systems;

3. **Enable Collaboration**: Provide a foundation for community-driven enhancements or adaptations of LPC, while maintaining fidelity to LPC's original design;

4. **Preserve Historical Context**: Document the features and design principles of LPC to ensure that the language’s original intent and functionality are not lost over time; and,

5. **Promote Education and Exploration**: Serve as a resource for programmers, hobbyists, and gamers interested in the role of LPC in the development of interactive gaming.

This specification is modeled after the scope and structure of modern programming language specifications but reflects LPC90’s simpler, more focused feature set. It aims to strike a balance between technical rigor and accessibility, making it useful for both technical audiences building LPC90-compliant compilers and systems and non-technical audiences interested in LPC’s legacy.

<h3 id="1.2">1.2 History of LPC <a href="#ch1">[toc]</a></h3>

Lars Pensj&ouml; [created LPC in 1989](https://w.wiki/CReE) as a streamlined programming language for MUD ("Multi-User Dungeon") game engine developers and world architects.  MUDs written in LPC came to be known, accordingly, as LPMuds.

<h3 id="1.3">1.3 Design Philosophy <a href="#ch1">[toc]</a></h3>

The original design of LPC (i.e., LPC90) reflected a pragmatic approach to programming for text-based, multi-user games, such as MUDs. Its philosophy was guided by simplicity, efficiency, and flexibility, aiming to empower developers to create and maintain complex, interactive systems with minimal overhead.

#### Key Principles

1. **C-like Simplicity**  
   LPC90 drew heavily from the syntax and semantics of the C programming language, providing developers with a familiar and straightforward programming style. This similarity reduced the learning curve for those already acquainted with C, while maintaining the readability and ease of use that procedural programming offered.

2. **Lightweight Object Orientation**  
   While not fully object-oriented, LPC90 introduced lightweight object support to facilitate modular design and code reuse. Objects encapsulated state and behavior, enabling developers to define interactive entities &emdash; such as players, items, and rooms &emdash; in a manner that was both intuitive and efficient.

3. **Performance for Real-Time Applications**  
   Designed for real-time, interactive environments, LPC90 prioritized performance. Its features were streamlined to minimize unnecessary complexity, ensuring that MUD servers could handle a high volume (by 1990 standards) of concurrent users and events without significant resource constraints.

4. **Flexibility and Extensibility**  
   LPC90 balanced simplicity with extensibility, providing mechanisms such as inheritance and preprocessor directives ('#include', '#define') to allow developers to structure and extend their code effectively. This flexibility supported a wide variety of use cases, from simple systems to complex game mechanics.

5. **Minimalism**  
   The language avoided overloading developers with unnecessary features, instead focusing on core functionality that aligned with its intended purpose. This minimalist design philosophy ensured that developers could focus on problem-solving rather than grappling with excessive language constructs.

6. **Preservation of Developer Creativity**  
   LPC90 provided developers with tools to implement custom behavior and mechanics without imposing rigid design patterns. This freedom fostered creativity and adaptability, enabling the development of highly customized and innovative MUDs.

#### Historical Context

LPC90's design reflected the state of computer hardware, networking, programming, and MUD development in the early 1990s. By blending the procedural style of C with lightweight object-oriented concepts, it provided a bridge between traditional structured programming and emerging object-oriented methodologies, making it uniquely suited to its era.

## 2. Lexical Structure  

<h3 id="2.1">2.1 Characters <a href="#ch2">[toc]</a></h3>

The **characters** used in LPC90 source code are defined by the standard ASCII character set. These characters are divided into the following categories based on their role in the language:

#### 1. **Letters**

- LPC90 recognizes the following as letters:
  - Uppercase letters: `A` to `Z`
  - Lowercase letters: `a` to `z`
- Letters are used in identifiers, keywords, and string literals.

#### 2. **Digits**
- The digits `0` to `9` are used in:
  - Numeric literals (e.g., `42`, `3.14`)
  - Identifiers (after the first character)

#### 3. **Whitespace**
- Whitespace characters are used to separate tokens and improve code readability. They include:
  - Space (` `)
  - Horizontal tab (`\t`)
  - Carriage return (`\r`)
  - Line feed (`\n`)
- Whitespace is ignored except when it separates tokens.

#### 4. **Special Characters**
- LPC90 uses the following special characters in its syntax:

```lpc
! " # $ % & ' ( ) * + , - . / : ; < = > ? [ \ ] ^ _ ` { | } ~
```

- These characters are used for operators, delimiters, and string literals.

#### 5. **Escape Sequences**
- Within string literals and character constants, the following escape sequences are recognized:
- `\\` - Backslash
- `\"` - Double quote
- `\n` - Line feed
- `\t` - Horizontal tab
- `\r` - Carriage return
- Additional escape sequences may be supported by the implementation for extended functionality.

#### 6. **Comments**
- Comments are ignored during lexical analysis and can span:
- A single line: Introduced by `//`
- Multiple lines: Enclosed between `/*` and `*/`

#### 7. **Character Encoding**
- LPC90 assumes the source file is encoded in ASCII. Any characters outside the standard ASCII range may lead to undefined behavior unless explicitly supported by the implementation.

#### 8. **Case Sensitivity**
- LPC90 is a case-sensitive language. For example:
  - The identifier `Variable` is distinct from `variable`.
- Keywords must be written in lowercase as specified.

---

### Example
Here is an example showcasing valid use of characters in LPC90:

```lpc
int count = 10;   // Variable declaration
string name = "LPC90\n";  /* String with escape sequence */
if (count > 0) {          // Special characters used in syntax
  count--;              // Decrement operator
}
```

<h3 id="2.2">2.2 Tokens <a href="#ch2">[toc]</a></h3>  

In LPC90, a **token** is the smallest unit of meaningful text in the source code. Tokens are recognized during lexical analysis and are categorized into several types:

#### 1. **Identifiers**
Identifiers are names used for variables, fields, methods, and other user-defined elements.  
- An identifier must begin with a letter (`A-Z`, `a-z`) or an underscore (`_`).  
- Subsequent characters may include letters, digits (`0-9`), or underscores.  
- Identifiers are case-sensitive.  

**Example**:  
```lpc
int my_varariable = 10;
string _name = "LPC90";
```

#### 2. **Keywords**
Keywords are reserved words that have predefined meanings in LPC90. They cannot be used as identifiers.  
Examples of keywords include:  
`if`, `else`, `for`, `while`, `return`, `true`, `false`, `nil`, `inherit`

**Example**:  
```lpc
if (x > 0) {
    return true;
}
```

#### 3. **Literals**
Literals represent fixed values in the source code. LPC90 supports the following types of literals:  
- **Integer literals**: Whole numbers, e.g., `42`, `-100`  
- **Float literals**: Decimal numbers, e.g., `3.14`, `-0.01`  
- **String literals**: Sequences of characters enclosed in double quotes, e.g., `"Hello World"`.  
- **Logical literals**: `true`, `false`, and `nil` (null).  

**Example**:  
```lpc
int num = 42;
float pi = 3.14;
string message = "Hello";
status flag = true;
```

#### 4. **Operators**
Operators are symbols that perform computations or comparisons. Examples include:  
- **Arithmetic Operators**: `+`, `-`, `*`, `/`, `%`  
- **Comparison Operators**: `==`, `!=`, `<`, `>`, `<=`, `>=`  
- **Logical Operators**: `&&`, `||`, `!`  
- **Assignment Operators**: `=`, `+=`, `-=`, `*=`, `/=`  

**Example**:  
```lpc
int result = 10 + 5;
if (x >= 0 && x < 100) {
    x += 1;
}
```

#### 5. **Delimiters**
Delimiters are symbols used to separate or group code elements. They include:  
- **Parentheses**: `(` and `)`  
- **Braces**: `{` and `}`  
- **Brackets**: `[` and `]`  
- **Semicolon**: `;`  
- **Comma**: `,`  
- **Colon**: `:`  

**Example**:  
```lpc
if (x > 0) {
    my_array[0] = 10;
}
```

#### 6. **Comments**
Comments are ignored by the compiler and are used for documentation:  
- Single-line comments begin with `//` and extend to the end of the line.  
- Multi-line comments are enclosed between `/*` and `*/`.  

**Example**:  
```lpc
// This is a single-line comment
/* This is a
   multi-line comment */
```

---

### Summary

Tokens are categorized as:  
1. **Identifiers**: Names of variables, fields, and methods.  
2. **Keywords**: Reserved words with predefined meanings.  
3. **Literals**: Fixed values such as numbers, strings, or logical constants.  
4. **Operators**: Symbols for computation, comparison, and logic.  
5. **Delimiters**: Symbols that structure the code.  
6. **Comments**: Non-executable documentation in the code.

The proper use of tokens ensures that LPC90 source code is well-formed and understandable by the compiler.

<h3 id="2.3">2.3 Keywords <a href="#ch2">[toc]</a></h3>  

Keywords in LPC90 are reserved words with predefined meanings. They are an essential part of the language syntax and cannot be used as identifiers for variables, methods, or other user-defined elements.

#### List of Keywords

The following words are reserved in LPC90:

- **Control Structures**:  
  `if`, `else`, `for`, `while`, `return`

- **Logical Constants**:  
  `true`, `false`, `nil`

- **Object-Oriented Keywords**:  
  `inherit`

#### Usage of Keywords

Keywords must be written in lowercase. LPC90 is case-sensitive, so writing `If` instead of `if` will result in a syntax error.

**Example**:  
```lpc
if (health > 0) {
    return true;
} else {
    return false;
}
```

In this example:  
- `if`, `else`, and `return` are keywords.  
- They control the flow of the program and are reserved for specific language behavior.

#### Restrictions
Attempting to use a keyword as an identifier will result in a compilation error. For example:

**Invalid Code**:
```lpc
int if = 10;  // Error: 'if' is a reserved keyword
```

---

### Summary

Keywords are reserved words that define the structure and behavior of LPC90 programs. They include control structures, logical constants, and object-oriented terms. Since LPC90 is case-sensitive, keywords must be written in lowercase exactly as specified.

<h3 id="2.4">2.4 Identifiers <a href="#ch2">[toc]</a></h3>  

Identifiers in LPC90 are names used to represent variables, methods, fields, parameters, and other user-defined elements. They allow developers to reference and manipulate data and behaviors in a program.

#### Rules for Identifiers

1. **Starting Character**:  
   An identifier must begin with:  
   - A letter (`A-Z`, `a-z`)  
   - An underscore (`_`)

2. **Subsequent Characters**:  
   After the first character, identifiers can include:  
   - Letters (`A-Z`, `a-z`)  
   - Digits (`0-9`)  
   - Underscores (`_`)

3. **Case Sensitivity**:  
   LPC90 is case-sensitive, meaning identifiers such as `Variable`, `variable`, and `VARIABLE` are treated as distinct.

4. **Reserved Words Restriction**:  
   Identifiers cannot be the same as keywords or reserved words (e.g., `if`, `else`, `return`). Using reserved words as identifiers will result in a compilation error.

#### Valid and Invalid Identifiers

**Valid Identifiers**:  
```lpc
int health;
string _name;
float player1_score;
```

**Invalid Identifiers**:  
```lpc
int 1stPlayer;   // Cannot start with a digit
float if;        // 'if' is a reserved keyword
string player-name; // Cannot contain a hyphen
```

---

### Naming Conventions

While LPC90 imposes no strict naming conventions, the following practices are encouraged to improve code readability:

1. **Use Descriptive Names**:  
   Choose names that clearly convey their purpose.  
   Example:  
   ```lpc
   int healthPoints;
   string playerName;
   ```

2. **Underscores for Separation**:  
   Use underscores to separate words in multi-word identifiers.  
   Example:  
   ```lpc
   float player_score;
   ```

3. **Avoid Reserved Words**:  
   Always avoid names that conflict with reserved keywords.

---

### Summary

Identifiers in LPC90:  
- Must start with a letter or an underscore.  
- Can include letters, digits, and underscores after the first character.  
- Are case-sensitive.  
- Cannot use reserved words.  

Adhering to these rules ensures that LPC90 programs are syntactically correct and readable.

<h3 id="2.5">2.5 Literals <a href="#ch2">[toc]</a></h3>  

<h3 id="2.6">2.6 Comments <a href="#ch2">[toc]</a></h3>

## 3. Types  

<h3 id="3.1">3.1 Primitive Types <a href="#ch3">[toc]</a></h3>  

<h3 id="3.2">3.2 Object Types <a href="#ch3">[toc]</a></h3>  

<h3 id="3.3">3.3 Special Types (`nil`, `mixed`) <a href="#ch3">[toc]</a></h3>  

<h3 id="3.4">3.4 Type Conversion <a href="#ch3">[toc]</a></h3>  

## 4. Variables  
<h3 id="4.1">4.1 Variable Declarations <a href="#ch4">[toc]</a></h3>  

<h3 id="4.2">4.2 Scope and Lifetime of Variables <a href="#ch4">[toc]</a></h3>  

<h3 id="4.3">4.3 Default Values <a href="#ch4">[toc]</a></h3>  

## 5. Operators  

<h3 id="5.1">5.1 Operator Precedence and Associativity <a href="#ch5">[toc]</a></h3>  

<h3 id="5.2">5.2 Arithmetic Operators <a href="#ch5">[toc]</a></h3>  

<h3 id="5.3">5.3 Relational and Logical Operators <a href="#ch5">[toc]</a></h3>  

<h3 id="5.4">5.4 Assignment Operators <a href="#ch5">[toc]</a></h3>  

## 6. Expressions  

<h3 id="6.1">6.1 Evaluation Order <a href="#ch6">[toc]</a></h3>  

<h3 id="6.2">6.2 Method Calls <a href="#ch6">[toc]</a></h3>  

<h3 id="6.3">6.3 Field Access <a href="#ch6">[toc]</a></h3>  

<h3 id="6.4">6.4 Conditional Expressions <a href="#ch6">[toc]</a></h3>  

## 7. Statements  

<h3 id="7.1">7.1 Block Statements <a href="#ch7">[toc]</a></h3>  

<h3 id="7.2">7.2 Control Flow Statements (`if`, `else`, `while`, `for`) <a href="#ch7">[toc]</a></h3>  

<h3 id="7.3">7.3 Return Statements <a href="#ch7">[toc]</a></h3>  

## 8. Objects  

<h3 id="8.1">8.1 Object Definition and Structure <a href="#ch8">[toc]</a></h3>  

<h3 id="8.2">8.2 Fields <a href="#ch8">[toc]</a></h3>  

<h3 id="8.3">8.3 Methods <a href="#ch8">[toc]</a></h3>  

<h3 id="8.4">8.4 Inheritance <a href="#ch8">[toc]</a></h3>  

## 9. Execution  

<h3 id="9.1">9.1 Program Entry Point <a href="#ch9">[toc]</a></h3>  

<h3 id="9.2">9.2 Object Instantiation and Initialization <a href="#ch9">[toc]</a></h3>  

## 10. Preprocessing Directives  

<h3 id="10.1">10.1 <code>#include</code> Directives<a href="#ch10">[toc]</a></h3>  

<h3 id="10.2">10.2 <code>#define</code> Macros <a href="#ch10">[toc]</a></h3>  

## 11. Error Handling  

<h3 id="11.1">11.1 Syntax Errors <a href="#ch11">[toc]</a></h3>  
  
<h3 id="11.2">11.2 Runtime Errors <a href="#ch11">[toc]</a></h3>  

## 12. Appendices

<h3 id="app-a">A. Backus-Naur Form (BNF) Grammar <a href="#appendices">[toc]</a></h3>

This appendix defines the grammar of LPC90 using Backus-Naur Form (BNF). The grammar specifies the structure of an LPC source file, which consists of the following elements in order:

1. Optional `inherit` declarations
2. Optional preprocessor directives, including `#include` and `#define`
3. Field declarations and definitions
4. Method declarations and definitions

#### A.1 BNF Grammar

```bnf
<source-file> ::= <inherit-section>? <preprocessor-section>? <field-section> <method-section>

<inherit-section> ::= "inherit" <string-literal> ";"

<preprocessor-section> ::= (<include-directive> | <define-directive>)*

<include-directive> ::= "#include" <file-path>
<file-path> ::= <quoted-file> | <bracketed-file>
<quoted-file> ::= "\"" <file-name> "\""
<bracketed-file> ::= "<" <file-name> ">"
<file-name> ::= <identifier> ("/" <identifier>)*

<define-directive> ::= "#define" <identifier> <replacement-text>

<field-section> ::= <field-declaration>*
<field-declaration> ::= <type> <identifier> ("=" <expression>)? ";"

<method-section> ::= <method-declaration>*
<method-declaration> ::= <type> <identifier> "(" <parameter-list>? ")" <block>
<parameter-list> ::= <parameter> ("," <parameter>)*
<parameter> ::= <type> <identifier>
<block> ::= "{" <statement>* "}"

<type> ::= "int" | "float" | "mapping" | "mixed" | "object" | "status" | "string" | "void"
<expression> ::= <literal> | <identifier> | <binary-expression> | <unary-expression>
<literal> ::= <integer-literal> | <float-literal> | <string-literal> | "true" | "false" | "nil"

<statement> ::= <expression> ";" 
              | "if" "(" <expression> ")" <block> ("else" <block>)?
              | "while" "(" <expression> ")" <block>
              | "for" "(" <expression>? ";" <expression>? ";" <expression>? ")" <block>
              | <block>
```

#### A.2 Example LPC Source File

```lpc
inherit "base_object";

#define MAX_HEALTH 100

#include "local_file.h"    // File in the same directory
#include <standard_lib.h>  // File in the standard library

int health = 100;
string name;

void reset() {
    health = MAX_HEALTH;
}
```

#### A.3 Parsing of the Example

The example LPC file in A.2 (above) parses into the following sections:

Inherit Section:
```lpc
inherit "base_object";
```

Preprocessor Section:
```lpc
#define MAX_HEALTH 100

#include "local_file.h" // File in the same directory
#include <standard_lib.h> // File in the standard library
```

Field Section:
```lpc
int health = 100;
string name;
```

Method Section:

```lpc
void reset() { health = MAX_HEALTH; }
```

<h3 id="app-b">B. Reserved Words <a href="#appendices">[toc]</a></h3>

This appendix lists the reserved words in LPC90. Reserved words are predefined keywords in the language that cannot be used as identifiers (such as variable names, function names, or object names). They are an integral part of the language syntax and semantics.

#### List of Reserved Words

The following words are reserved in LPC90:

- **Data Types**:
  - `int`
  - `float`
  - `mapping`
  - `mixed`
  - `object`
  - `status`
  - `string`
  - `void`

- **Control Structures**:
  - `else`
  - `for`
  - `if`
  - `return`
  - `while`

- **Logical Constants**:
  - `false`
  - `nil`
  - `true`

- **Object-Oriented Keywords**:
  - `inherit`

#### Notes

1. **Case Sensitivity**:
   LPC90 is a case-sensitive language. Reserved words must be written in lowercase as listed above.

2. **Future Extensions**:
   Additional reserved words may be introduced in future versions of the LPC specification. Programs written in LPC90 should avoid using words that might reasonably become reserved in future specifications, such as `switch` or `class`.

3. **Impact on Identifiers**:
   Because reserved words cannot be redefined, attempting to use them as identifiers will result in a compilation error.
   
Editor's note:  The draft LPC90 specification was generated with the assistance of ChatGPT.
