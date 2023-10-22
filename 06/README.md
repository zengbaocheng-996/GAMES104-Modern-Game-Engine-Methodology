# Reflection System

In computer science, reflective programming or reflection is the ability of a process to examine, introspect, and modify its own structure and behavior.

1. Collect type info from code

   generate schema from AST (Clang -> Abstract Syntax Tree)

   precise control of reflection scope (use macro to add reflection controls)

2. Generate code to provide accessors for fields and methods

   reflection accessors (get, set, invoke)

   code rendering (mustache)

3. Manage all accessors with a <string, accessor> map

|                | Download                                                   |
| -------------- | ---------------------------------------------------------- |
| Piccolo Engine | https://github.com/BoomingTech/Piccolo/releases/tag/v0.0.9 |

| Modified File Name                         |
| ------------------------------------------ |
| motor_component.h<br />motor_component.cpp |
| lua_component.h<br />lua_component.cpp     |
| player.object.json                         |
| method.h<br />method.cpp                   |
| meta_data_config.h                         |
| class.h<br />class.cpp                     |
| commonReflectionFile.mustache              |
| generate.cpp                               |
| reflection.h<br />reflection.cpp           |

