# Start options

## Engine
In order to pass some additional flags when launching engine use '-'.  
Example: ***Duckvil.exe -server***.
- ### server
  Run engine as server, so other engines will be able to connect to your engine.
- ### client
  Run engine as client, so you will be able to connect to other engine.
- ### project *project_name*
  Load specified by ***project_name*** project at startup.

## Reflection generator
- ### CWD
  **Should be always set.**  
  Set current working directory. It should be root project path.
- ### file
  If set, only this file will be processed.
- ### is_relative
  Set if path is relative to CWD.
- ### is_absolute
  Set if path is absolute.
- ### force
  Force reflection regeneration. *reflection_db.json* file will be ignored.
- ### single
  Set if project has single module architecture.
