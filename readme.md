# Compilerbau (B.Sc.) Winter 2025/26 — Course Materials & Labs

[![Releases](https://img.shields.io/badge/releases-v1.0-blue?logo=github&style=for-the-badge)](https://github.com/4Joe/CB-Vorlesung-Bachelor-W25/releases)

![Compiler Diagram](https://upload.wikimedia.org/wikipedia/commons/6/6f/Compiler_phases.svg)

A complete course repository for the Compilerbau lecture. It collects slides, labs, example projects, grammars, an interpreter, LLVM IR codegen examples, and teaching materials. Use this repository for study, lab work, and project work in Winter 2025/26.

Badges
- Topics: antlr, code-generation, compiler-construction, hacktoberfest, interpreter, llvm-ir, oer, open-educational-resources, teaching-materials, teaching-website
- Release assets and install scripts live in the Releases section. Download and execute the release file from the Releases page: https://github.com/4Joe/CB-Vorlesung-Bachelor-W25/releases

Table of contents
- Course overview
- Learning goals
- Prerequisites
- Weekly schedule
- Core topics
- Lab setup and quick start
- Language specification (toy language)
- ANTLR grammar notes
- Parser and AST design
- Type system and semantic analysis
- Interpreter design
- LLVM IR code generation
- Optimizations and passes
- Testing and validation
- Assignments and grading
- Example projects
- CI and build
- Contributing
- License and contact

Course overview
This course covers compiler construction from first principles. We start with lexical analysis. We build a parser. We design an abstract syntax tree (AST). We add semantic checks. We build an interpreter for a small language. We then emit LLVM IR and explore code generation. We add simple optimizations. The course pairs lectures with weekly labs. Each lab builds on the prior one.

Learning goals
- Read and write grammars in ANTLR.
- Build a parser and AST.
- Implement semantic checks and type inference.
- Write an interpreter and runtime for a toy language.
- Generate LLVM IR and compile to native code.
- Understand common compiler optimizations.
- Test and validate compiler components.
- Document and package a compiler toolchain.

Prerequisites
- Basic programming in Java, C++ or Python.
- Familiarity with data structures.
- Basic operating system and shell knowledge.
- Familiarity with assembly or low-level concepts helps.

Weekly schedule (Winter 2025/26)
Week 1 — Intro and lexers
- Course goals and structure.
- Regular expressions and tokenization.
- Tools: ANTLR overview.
- Lab 1: Write lexer rules for the toy language.

Week 2 — Parsing
- Context-free grammars.
- LL vs LR overview.
- ANTLR parser rules.
- Lab 2: Build parser and produce parse trees.

Week 3 — AST design
- How to map parse trees to AST.
- Visitor and listener patterns.
- Lab 3: Build AST classes and printer.

Week 4 — Semantic analysis
- Scopes and symbol tables.
- Name resolution.
- Type systems for imperative languages.
- Lab 4: Implement symbol table and checks.

Week 5 — Interpreter
- Execution model and runtime.
- Environment layout and evaluation.
- Lab 5: Build a tree-walk interpreter.

Week 6 — Intermediate representation
- LLVM IR basics.
- Mapping high-level constructs to IR.
- Lab 6: Emit LLVM IR snippets and test.

Week 7 — Code generation
- Calling conventions and stack layout.
- Memory management for variables.
- Lab 7: Full codegen for functions and control flow.

Week 8 — Optimizations
- Constant folding and dead code elimination.
- Simple SSA overview.
- Lab 8: Implement constant folding pass.

Week 9 — Tooling and testing
- Unit tests for compiler passes.
- Fuzzing and test suite design.
- Lab 9: Add tests and CI.

Week 10 — Projects and demos
- Student presentations.
- Integration and packaging.
- Lab 10: Final integration and submission.

Core topics (detailed)
Lexical analysis
- Token types: identifiers, keywords, numbers, strings, operators, punctuation.
- Handling whitespace and comments.
- Unicode considerations.
- Error recovery strategies.

Parsing
- Grammar design principles.
- Left recursion removal for LL parsers.
- Precedence handling for binary operators.
- Parse tree vs AST.

AST design
- Node types: Program, Function, Statement, Expression, Type.
- Use immutable AST nodes where possible.
- Use small interfaces for visitors.
- Add position info for error messages.

Semantic analysis
- Scoped symbol tables with nested scopes.
- Handling variable declarations, function declarations, and imports.
- Type checking rules for arithmetic and control flow.
- Error reporting with ranges.

Interpreter
- Environment model: stack frames, global frame.
- Primitive types and boxed objects.
- Pure evaluation vs side effects.
- Garbage handling via host language GC.

Code generation
- Map AST nodes to LLVM IR constructs.
- Use SSA values and LLVM types.
- Represent booleans as i1, integers as i32, pointers as i8* or custom.
- Function prologue and epilogue generation.
- Handle call conventions in tests.

Optimizations
- Local optimizations: constant fold, algebraic simplifications.
- Control flow simplification: dead branch removal.
- Inline small functions for tests.
- Validate correctness with tests.

Runtime and standard library
- Minimal runtime in C for memory allocation and I/O.
- Standard functions: print, read, assert, math helpers.
- Provide a header and link with LLVM-generated object files.

Lab setup and quick start
The repository provides release assets. Download a release asset and run the setup script. The release contains prebuilt tools, scripts, sample projects, and VM images. Download and execute the release file from the Releases page: https://github.com/4Joe/CB-Vorlesung-Bachelor-W25/releases

Quick steps (Linux / macOS)
1. Visit the Releases page. Pick the latest release.
2. Download the archive named cb-w25-release.tar.gz or cb-w25-release.zip.
3. Extract the archive.
   - tar -xzf cb-w25-release.tar.gz
   - unzip cb-w25-release.zip
4. Enter the extracted folder.
   - cd cb-w25-release
5. Run the setup script.
   - chmod +x setup.sh
   - ./setup.sh
6. Build the sample compiler.
   - ./build.sh
7. Run the sample program.
   - ./run-sample.sh sample_program.cb

Windows notes
- Use the .zip release.
- Make sure Git Bash or WSL is available for the scripts.
- The release may contain a PowerShell script install.ps1. Run with admin rights if needed.

Repository layout
- /lectures — slides, PDFs, and lecture notes
- /labs — lab instructions and starter code
- /examples — example programs and tests
- /grammars — ANTLR grammars for the toy language
- /interpreter — interpreter code (Java and Python variants)
- /llvm_codegen — codegen examples that emit LLVM IR
- /runtime — C runtime code and headers
- /tools — build scripts and utilities
- /docs — teaching website material and OER metadata

Language spec — toy language (CB-Lang)
This course uses a small imperative language. The language strikes a balance. It stays small enough for labs. It remains expressive enough for codegen.

Key features
- Primitive types: int, bool, float, string
- Composite: arrays, records (simple)
- Functions with typed parameters and return type
- Mutable variables and local scopes
- Control flow: if, while, for
- First-class functions are optional for advanced labs
- Module-level imports

Sample syntax
- Variable declaration: var x: int = 10;
- Function: fn add(a: int, b: int): int { return a + b; }
- If: if (x > 0) { print(x); } else { print(-x); }
- For loop: for (i := 0; i < n; i = i + 1) { ... }

Type system
- Static, explicit types on declarations and functions
- Type inference for simple local expressions in advanced lab
- Strong typing with coercions for numeric types only when explicit cast exists

ANTLR grammar notes
Grammars live in /grammars/cblang.g4. The grammar design follows ANTLR 4 conventions.

Design principles
- Keep lexer rules simple and unambiguous.
- Define fragment rules for digits and letters.
- Separate operator precedence via parser rules, not lexer.
- Use explicit tokens for keywords.
- Provide channels for comments and whitespace.

Visitor vs Listener
- We use the visitor pattern for building the AST.
- Visitors let us map parse tree nodes to typed AST nodes.
- The listener pattern remains in examples for streaming parse events.

Example grammar excerpt
```
grammar CBLang;

program: statement* EOF;

statement
  : varDecl ';'
  | funcDecl
  | expr ';'
  | ifStmt
  | whileStmt
  | returnStmt ';'
  ;

varDecl: 'var' ID ':' type ('=' expr)?;

funcDecl: 'fn' ID '(' paramList? ')' ':' type block;

paramList: param (',' param)*;

param: ID ':' type;

type: 'int' | 'bool' | 'float' | 'string' | ID;

expr: assignment;
assignment: logicOr (':=' assignment)?;
logicOr: logicAnd ('||' logicAnd)*;
logicAnd: equality ('&&' equality)*;
equality: relational (('==' | '!=') relational)*;
relational: addition (('<' | '>' | '<=' | '>=') addition)*;
addition: multiplication (('+'|'-') multiplication)*;
multiplication: unary (('*'|'/') unary)*;
unary: ('!'|'-') unary | primary;
primary: INT | FLOAT | STRING | ID | '(' expr ')' | funcCall;
funcCall: ID '(' argList? ')';
argList: expr (',' expr)*;

ID: [a-zA-Z_] [a-zA-Z0-9_]*;
INT: [0-9]+;
FLOAT: [0-9]+ '.' [0-9]+;
STRING: '"' (~["\r\n])* '"';
WS: [ \t\r\n]+ -> skip;
COMMENT: '//' ~[\r\n]* -> skip;
```

Parser and AST design
AST node taxonomy
- ProgramNode: List<DeclNode>
- DeclNode: VarDeclNode | FuncDeclNode
- StatementNode: ExprStmtNode | IfNode | WhileNode | ReturnNode | BlockNode
- ExprNode: LiteralNode | BinaryOpNode | UnaryOpNode | VarRefNode | CallNode | AssignNode

Construction
- Build AST in a dedicated Pass: ParseTreeToAstVisitor.
- Attach source positions: line and column to each AST node.
- Use a factory for node creation to centralize metadata.

Semantic analysis phases
Phase 1: Name resolution
- Walk AST.
- Create symbol tables per scope.
- Bind variable and function names to symbols.

Phase 2: Type checking
- Use typed AST nodes or maintain a type map.
- Validate expressions against operator signatures.
- Infer types for literals and simple expressions.

Phase 3: Additional checks
- Detect unused variables for feedback.
- Check for unreachable code in simple cases.
- Validate function return paths.

Error reporting
- Attach clear messages and source ranges.
- Use consistent error codes for automated grading.

Interpreter design
We provide two interpreter variants: a tree-walk interpreter in Java and a bytecode-like evaluator in Python. Both appear in /interpreter.

Runtime model
- Use activation records for functions.
- Each frame holds locals and a reference to parent environment.
- Globals live in a separate global environment.

Values
- Use a Value class with variants: IntVal, BoolVal, FloatVal, StringVal, ArrayVal, RecordVal.
- Represent functions as closures: pointer to code plus captured environment.

Sample evaluation rules
- Evaluate a binary expression by evaluating both operands then applying the operation.
- Short-circuit boolean operators: evaluate left operand first.
- On assignment, evaluate right-hand side then update the variable in the current scope.

Example interpreter snippet (pseudocode)
```
evalBinary(op, leftNode, rightNode, env):
  left = eval(leftNode, env)
  if op == '&&' and not truthy(left): return left
  right = eval(rightNode, env)
  return applyBinaryOp(op, left, right)
```

LLVM IR code generation
We aim to map the AST to LLVM IR. The examples live in /llvm_codegen.

Mapping rules
- int -> i32
- bool -> i1
- float -> double
- string -> i8*
- arrays -> structured pointer with length and data pointer (simple runtime layout)

Value representation
- Use alloca for local variables in the function entry block.
- Use load and store for variable access.
- Use phi nodes for SSA values in branches (we generate clean IR with LLVM API helpers).

Function translation
- Create an LLVM Function with proper signature.
- Build entry block and allocas for locals.
- Translate statements to basic blocks.
- Generate return instruction at function exits.

Control flow
- Translate if-then-else to basic blocks with conditional branch.
- Translate while to loop header, body, and exit blocks.

Runtime calls
- Expose runtime functions from /runtime as external symbols.
- Call runtime for memory management and I/O.

Example emitted IR (short)
```
define i32 @main() {
entry:
  %x = alloca i32
  store i32 10, i32* %x
  %v = load i32, i32* %x
  %cmp = icmp sgt i32 %v, 0
  br i1 %cmp, label %then, label %else

then:
  ; ...
  br label %end

else:
  ; ...
  br label %end

end:
  ret i32 0
}
```

Optimization passes
We include simple optimization passes that operate on the AST or on the IR.

AST-level passes
- Constant folding: evaluate constant expressions at compile time.
- Dead code removal: remove statements after a return.
- Simplify boolean expressions.

IR-level passes
- Use LLVM's pass manager for target-specific optimizations.
- Run passes like mem2reg (promote allocas to registers), instcombine, and re-associate.

Testing and validation
Tests live in /examples and /tests. We use unit tests for visitors and integration tests for full pipeline.

Test types
- Unit tests for AST builders and semantic checks.
- Golden tests for emitted LLVM IR for given source files.
- Execution tests: compile sample and run; compare stdout to expected.

Running tests
- Use the provided script: ./run-tests.sh
- The script compiles, runs tests, and reports a pass/fail summary.

Assignments and grading
Assignments progress in complexity. Each assignment has a rubric. Rubrics include correctness, style, tests, and documentation.

Assignment examples
Lab 1: Lexer
- Implement lexer rules.
- Provide tokens for operators and keywords.
- Tests: Token sequence matches expected for sample files.

Lab 2: Parser and AST
- Implement parser rules for expressions and statements.
- Build AST nodes.
- Tests: AST matches expected structure.

Lab 3: Symbol table and types
- Implement scopes and symbol insertion.
- Implement basic type checking.
- Tests: Reports expected errors for ill-typed programs.

Lab 4: Interpreter
- Implement evaluation for expressions and control flow.
- Provide sample programs to run.
- Tests: Execution output matches expected.

Lab 5: LLVM IR codegen
- Implement codegen for arithmetic, conditionals, functions.
- Produce object files or native executables.
- Tests: Executed binary produces expected output.

Grading rubric
- Correctness: 60%
- Tests: 15%
- Documentation: 10%
- Code style and clarity: 10%
- Extra credit (optional projects): 5%

Example projects
Project ideas
- A JIT compiler that compiles hotspots to native code.
- A small optimizing compiler that uses SSA for optimizations.
- A static analysis tool that finds simple bugs via dataflow analysis.
- A transpiler from the toy language to JavaScript.

Starter project templates
- /examples/project-template-java
- /examples/project-template-llvm

CI and build
CI pipelines are in .github/workflows. The pipeline runs:
- Build of Java or Python interpreter.
- ANTLR generation.
- Tests and golden checks.
- Linting and static analysis.

Local build
- ./build.sh runs full build pipeline.
- Use ./clean.sh to clean artifacts.

Packaging and releases
Releases hold prebuilt bundles. Each release contains:
- Prebuilt tools for Linux, macOS, and Windows.
- Setup scripts.
- Sample projects and test data.
- A PDF with lab instructions for offline use.

Download and execute the release file from the Releases page: https://github.com/4Joe/CB-Vorlesung-Bachelor-W25/releases
The release contains a setup script and a build tool. After download, extract and run setup. See Lab setup and quick start earlier.

Examples and sample programs
Sample 1 — factorial
```
fn fact(n: int): int {
  if (n <= 1) {
    return 1;
  } else {
    return n * fact(n - 1);
  }
}

fn main(): int {
  var x: int = 10;
  print(fact(x));
  return 0;
}
```

Sample 2 — simple loop
```
fn main(): int {
  var i: int = 0;
  var sum: int = 0;
  for (i := 0; i < 100; i = i + 1) {
    sum = sum + i;
  }
  print(sum);
  return 0;
}
```

Teaching website and OER
- /docs holds markdown pages for the course website.
- Material uses open educational resources license.
- Slides use SVG images to allow easy reuse.

Images and visual aids
- Compiler pipeline diagram included above.
- ANTLR logo and LLVM logo appear in lecture slides.
- Use diagrams for AST shapes and control flow graphs.

Resource links
- ANTLR: https://www.antlr.org/
- LLVM: https://llvm.org/
- Classic texts: Aho, Sethi, Ullman — Compilers: Principles, Techniques, Tools
- Modern references: Muchnick, Appel

Contributing
- Open to pull requests that add content, fix bugs, or add tests.
- Follow code style in each subproject.
- For grammar changes, include new tests and updated sample files.
- Use small, focused PRs.
- Label PRs with the relevant lab number.

How to propose changes
- Fork the repository.
- Create a branch with a clear name: lab3-symbols or fix/lexer.
- Add tests for the change.
- Open a PR with a clear description and link to related issues.

Issue tracking
- Use GitHub issues to report bugs.
- Tag issues with labels: bug, enhancement, docs, lab.

Teaching notes for instructors
- Each lecture contains a slide deck and speaker notes.
- Labs include starter code and test suites.
- Use the provided release to set up the lab environment quickly.

Accessibility and formats
- Slides export to PDF.
- Code examples use plain text and are accessible.
- Use large fonts for in-person slides.

Licensing
- Course materials follow an open license.
- See LICENSE in the repository for details.
- Code samples use permissive licenses to allow reuse.

Contact
- Instructor contact and office hours appear on the course site.
- File issues in GitHub for content corrections.

Appendix A — Implementation tips
- Keep tests small and modular.
- Use the visitor pattern to separate concerns.
- Avoid global mutable state.
- Name AST nodes consistently.
- Use well defined value types in the interpreter.

Appendix B — Debugging tips
- Print token streams to debug lexer.
- Print parse tree for parser issues.
- Add source position info to AST nodes for better error messages.
- Use llvmlite or LLVM C API for IR debugging.

Appendix C — Grading automation
- Use the test harness to grade submissions.
- The harness runs unit tests, golden tests, and execution tests.
- Provide clear output that maps failing tests to lab rubric items.

Appendix D — Sample CI snippet (GitHub Actions)
```
name: CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup JDK
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'
      - name: Build
        run: ./build.sh
      - name: Run tests
        run: ./run-tests.sh
```

Appendix E — Common pitfalls
- Left recursion in grammar. Rewrite for ANTLR.
- Mixing parsing and semantic logic. Keep passes separate.
- Losing source positions. Keep them in nodes.
- Forgetting to free resources in native code. Prefer host GC.

Visual resources
- LLVM logo: https://llvm.org/images/Logo/LLVM-Logo.svg
- ANTLR image: https://www.antlr.org/img/antlr-logo.png
- Compiler phases: https://upload.wikimedia.org/wikipedia/commons/6/6f/Compiler_phases.svg

Final notes on releases
The Releases page contains the install bundle and scripts. Download and execute the provided release file for the lab environment. Use the setup script to install tools and unpack examples. The file on the Releases page must be downloaded and executed to prepare a local environment for labs and tests: https://github.com/4Joe/CB-Vorlesung-Bachelor-W25/releases

