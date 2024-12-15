---
layout: default
title: LPC90 Language Specification
---

# LPC90 Language Specification

## Table of Contents

1. **Introduction**  
   1.1 [Purpose of this Specification](#11-purpose-of-this-specification)  
   1.2 [History of LPC](#12-history-of-lpc)  
   1.3 Design Philosophy  

3. **Lexical Structure**  
   2.1 Characters  
   2.2 Tokens  
   2.3 Keywords  
   2.4 Identifiers  
   2.5 Literals  
   2.6 Comments  

4. **Types**  
   3.1 Primitive Types  
   3.2 Object Types  
   3.3 Special Types (`nil`, `mixed`)  
   3.4 Type Conversion  

5. **Variables**  
   4.1 Variable Declarations  
   4.2 Scope and Lifetime of Variables  
   4.3 Default Values  

6. **Operators**  
   5.1 Operator Precedence and Associativity  
   5.2 Arithmetic Operators  
   5.3 Relational and Logical Operators  
   5.4 Assignment Operators  

7. **Expressions**  
   6.1 Evaluation Order  
   6.2 Method Calls  
   6.3 Field Access  
   6.4 Conditional Expressions  

8. **Statements**  
   7.1 Block Statements  
   7.2 Control Flow Statements (`if`, `else`, `while`, `for`)  
   7.3 Return Statements  

9. **Objects**  
   8.1 Object Definition and Structure  
   8.2 Fields  
   8.3 Methods  
   8.4 Inheritance  

10. **Execution**  
   9.1 Program Entry Point  
   9.2 Object Instantiation and Initialization  

11. **Preprocessing Directives**  
   10.1 `#include` Directives  
   10.2 `#define` Macros  

12. **Error Handling**  
   11.1 Syntax Errors  
   11.2 Runtime Errors  

13. **Appendices**  
   A. [Backus-Naur Form (BNF) Grammar](#backus-naur-form-bnf-grammar)
      A.1 BNF Grammar
    A.2 Example LPC Code
   B. [Reserved Words](#reserved-words)  

## 1. Introduction

### 1.1 Purpose of this Specification

The purpose of this specification is to define the syntax, semantics, and structure of LPC, a programming language designed for building and enhancing LPMUDs (online, multi-user, text-only role-playing games) &mdash; specifically, as the language existed very soon after its inception. By offering a formal and detailed description of LPC circa 1990, the LPC90 language specification aims to:

1. **Establish a Foundation**: Establish a consistent and widely accepted foundation that describes an "original" dialect of LPC, providing a common starting point from which future LPC90-based specifications can evolve;

2. **Facilitate Compatibility**: Provide a clear and consistent reference for developers working with or adapting legacy LPC-based systems;

3. **Enable Collaboration**: Provide a foundation for community-driven enhancements or adaptations of LPC, while maintaining fidelity to LPC's original design;

4. **Preserve Historical Context**: Document the features and design principles of LPC to ensure that the language’s original intent and functionality are not lost over time; and,

5. **Promote Education and Exploration**: Serve as a resource for programmers, hobbyists, and gamers interested in the role of LPC in the development of interactive gaming.

This specification is modeled after the scope and structure of modern programming language specifications but reflects LPC90’s simpler, more focused feature set. It aims to strike a balance between technical rigor and accessibility, making it useful for both technical audiences building LPC90-compliant compilers and systems and non-technical audiences interested in LPC’s legacy.

### 1.2 History of LPC
Lars Pensj&ouml; is credited with [creating LPC in 1989](https://w.wiki/CReE) as a simple, C-like programming language for developers of LPMUD game drivers and worlds.

---


## 13. Appendices

### A. Backus-Naur Form (BNF) Grammar

This appendix defines the grammar of LPC90 using Backus-Naur Form (BNF). The grammar specifies the structure of an LPC source file, which consists of the following elements in order:

1. Optional `inherit` declarations
2. Optional preprocessor directives, including `#include` and `#define`
3. Field declarations and definitions
4. Method declarations and definitions

A.1 BNF Grammar

```bnf
<source-file> ::= <inherit-section>? <preprocessor-section>? <field-section> <method-section>

<inherit-section> ::= "inherit" <string-literal> ";"

<preprocessor-section> ::= (<include-directive> | <define-directive>)*
<include-directive> ::= "#include" <string-literal>
<define-directive> ::= "#define" <identifier> <replacement-text>

<field-section> ::= <field-declaration>*
<field-declaration> ::= <type> <identifier> ("=" <expression>)? ";"

<method-section> ::= <method-declaration>*
<method-declaration> ::= <type> <identifier> "(" <parameter-list>? ")" <block>
<parameter-list> ::= <parameter> ("," <parameter>)*
<parameter> ::= <type> <identifier>
<block> ::= "{" <statement>* "}"

<type> ::= "int" | "float" | "string" | "status" | "object" | "mapping" | "mixed" | "void"
<expression> ::= <literal> | <identifier> | <binary-expression> | <unary-expression>
<literal> ::= <integer-literal> | <float-literal> | <string-literal> | "true" | "false" | "nil"

<statement> ::= <expression> ";" 
              | "if" "(" <expression> ")" <block> ("else" <block>)?
              | "while" "(" <expression> ")" <block>
              | "for" "(" <expression>? ";" <expression>? ";" <expression>? ")" <block>
              | <block>
```

A.2 Example LPC Source File

```lpc
inherit "base_object";

#define MAX_HEALTH 100
#include "constants.h"

int health = 100;
string name;

void reset() {
    health = MAX_HEALTH;
}
```

A.3 Explanation of the Example

The example LPC file parses into the following sections:

Inherit Section:
```lpc
inherit "base_object";
```

Preprocessor Section:
```lpc
#define MAX_HEALTH 100
#include "constants.h"
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

B. ### Reserved Words

This appendix lists the reserved words in LPC90. Reserved words are predefined keywords in the language that cannot be used as identifiers (such as variable names, function names, or object names). They are an integral part of the language syntax and semantics.

## List of Reserved Words

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

## Notes

1. **Case Sensitivity**:
   LPC90 is a case-sensitive language. Reserved words must be written in lowercase as listed above.

2. **Future Extensions**:
   Additional reserved words may be introduced in future versions of the LPC specification. Programs written in LPC90 should avoid using words that might reasonably become reserved in future specifications, such as `switch` or `class`.

3. **Impact on Identifiers**:
   Because reserved words cannot be redefined, attempting to use them as identifiers will result in a compilation error.

