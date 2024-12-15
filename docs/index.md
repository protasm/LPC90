---
layout: default
title: LPC90 Language Specification
---

# LPC90 Language Specification

## Table of Contents

1. **Introduction**  
   1.1 [Purpose of this Specification](#purpose-of-this-specification)  
   1.2 [History of LPC](#history-of-lpc)  
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
   A. Backus-Naur Form (BNF) Grammar  
   B. Reserved Words  

## Purpose of this Specification

The purpose of this specification is to define the syntax, semantics, and structure of LPC, a programming language designed for building and enhancing LPMUDs (online, multi-user, text-only role-playing games) &mdash; specifically, as the language existed very soon after its inception. By offering a formal and detailed description of LPC circa 1990, the LPC90 language specification aims to:

1. **Establish a Foundation**: Establish a consistent and widely accepted foundation that describes as the "original" dialect of LPC, providing a common starting point from which future LPC specifications can evolve;

2. **Facilitate Compatibility**: Provide a clear and consistent reference for developers working with or adapting legacy LPC-based systems;

3. **Enable Collaboration**: Provide a foundation for community-driven enhancements or adaptations of LPC90, while maintaining fidelity to LPC's original design;

4. **Preserve Historical Context**: Document the features and design principles of LPC to ensure that the language’s original intent and functionality are not lost over time; and,

5. **Promote Education and Exploration**: Serve as a resource for programmers, hobbyists, and gamers interested in the role of LPC in the development of interactive gaming.

This specification is modeled after the scope and structure of modern programming language specifications but reflects LPC90’s simpler, more focused feature set. It aims to strike a balance between technical rigor and accessibility, making it useful for both technical audiences building LPC90-compliant compilers and systems and non-technical audiences interested in LPC’s legacy.

## History of LPC
Lars Pensj&ouml; is credited with [creating LPC in 1989](https://w.wiki/CReE) as a simple, C-like programming language for developers of LPMUD game drivers and worlds.
