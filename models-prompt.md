**🧱 Role:**
You are an expert in Delphi/Lazarus programming and mORMot v2.2 architecture. You systematically apply the SOLID principles, particularly the Liskov Substitution Principle, to ensure robust and maintainable abstraction layers.

**🔍 Mission Objective:**
Based on the previous OpenAPI (YAML) definition, generate a complete mORMot v2.2–based project including:

1. TOrm models
2. SOA interfaces (I...Service)
3. Implementation classes (T...Service)
4. Node servers (T...Server)
5. A main HTTP server (THttpServerMain)
6. A main program (ServerApi.dpr)

**📊 Requested Generation Steps:**

1. 📒 **OpenAPI Validation:**

   * Load and parse the provided OpenAPI document.
   * Analyze each schema, path, and HTTP operation.

2. 🕊️ **Delphi Models (TOrm):**

   * Generate one TOrm class per schema, respecting data types (RawUtf8, Int64, TDateTime, Boolean, etc.).
   * Apply `stored AS_UNIQUE` and `index ...` if constraints are defined.
   * Inherit all models from `TOrmTimeStamped` for automatic timestamp management.

3. 📄 **DTOs (if present):**

   * Generate corresponding `packed record` types for DTOs.
   * Use `Rtti.RegisterFromText()` for custom serialization.

4. 🚀 **Service Interfaces (I...Service):**

   * For each REST path, define a method in an `IInvokable` interface.
   * Annotate HTTP verbs (\[get], \[post], etc.) via comments for mORMot.
   * Define the expected return type as `TServiceCustomAnswer`.

5. 🚃 **Implementation Classes (T...Service):**

   * Implement CRUD logic for each service.
   * Perform data validation (e.g., non-empty titles).
   * Structure responses with `Result.Content := JsonEncode(...)`.
   * Include optional logging and precise error handling.

6. 🛋 **mORMot TRestServerDB Setup for Each Module:**

   * Initialize a `TOrmModel` instance.
   * Configure `CreateMissingTables`, `AcquireExecutionMode`, and `ServiceDefine(..., sicShared)`.

7. 🚧 **Main HTTP Server:**

   * Create `THttpServerMain` to instantiate all module servers.
   * Configure `TRestHttpServer` with JWT support and `OnBeforeBody` callbacks.

8. 💻 **Final Server Program (ServerApi.dpr):**

   * Implement a console application that starts `THttpServerMain`.
   * Output the available routes and port number to the console.

**✨ Quality Guidelines:**

* Use `TJWTS3256` for JWT handling.
* Always separate DTO types from TOrm models when their structures differ.
* Provide detailed comments for all classes and methods.
* Never hardcode sensitive constants.
* Use `TAutoLocker` for thread safety where appropriate.

**📚 mORMot v1 → v2 Migration Map:**

| mORMot1 Name                      | mORMot2 Unit                         | mORMot2 Name                              |
| --------------------------------- | ------------------------------------ | ----------------------------------------- |
| \_JSON                            | mormot.core.variants                 |                                           |
| \_ObjFast                         | mormot.core.variants                 |                                           |
| AS\_UNIQUE                        | mormot.orm.base                      |                                           |
| CompressGZip                      | mormot.core.zip                      |                                           |
| DBServerAccessRight               |                                      | RestServerAccessRight                     |
| DoubleToStr                       | mormot.core.text                     |                                           |
| FormatUTF8                        | mormot.core.text<br>mormot.core.json |                                           |
| GetEnumName                       | mormot.core.rtti                     |                                           |
| GetEnumNameValue                  | mormot.core.rtti                     |                                           |
| GetFileNameWithoutExt             | mormot.core.os                       |                                           |
| GetJSONFieldOrObjectOrArray       | mormot.core.json                     | TGetJsonField.GetJSONFieldOrObjectOrArray |
| GotoNextNotSpace                  | mormot.core.text                     |                                           |
| IdemPropNameU                     | mormot.core.unicode                  |                                           |
| INITIALIZETABLE\_NOINDEX          | mormot.orm.base                      |                                           |
| Int32ToUtf8                       | mormot.core.text                     |                                           |
| IsHtmlContentTypeTextual          | mormot.core.data                     |                                           |
| ISynLog                           | mormot.core.log                      |                                           |
| j2o\*                             | mormot.core.json                     | jpo\*                                     |
| JSON\_OPTIONS\_FAST               | mormot.core.variants                 | JSON\_FAST                                |
| JSONArrayItem                     | mormot.core.json                     |                                           |
| JsonObjectByPath                  | mormot.core.json                     |                                           |
| JsonObjectItem                    | mormot.core.json                     |                                           |
| JSONToObject                      | mormot.core.json                     |                                           |
| NewParallelProcess                | mormot.rest.core                     | Run.NewParallelProcess                    |
| PDocVariantData                   | mormot.core.variants                 |                                           |
| PosEx                             | mormot.core.base                     |                                           |
| ptIdentifiedInOnFile              | mormot.core.log                      | ptIdentifiedInOneFile                     |
| PUTF8Char                         | mormot.core.base                     |                                           |
| RawByteString                     | mormot.core.base                     |                                           |
| RawUTF8                           | mormot.core.base                     |                                           |
| RotateFileNoCompression           | mormot.core.log                      |                                           |
| secSSL                            | mormot.rest.http.server              | secTLS                                    |
| SendEmail                         | mormot.net.client                    |                                           |
| ServiceLog                        |                                      | WindowsServiceLog                         |
| ServicesRun                       | mormot.core.os                       | ServiceSingleRun                          |
| SockString                        | mormot.core.base                     | RawUTF8                                   |
| SQLAddWhereAnd                    | mormot.db.core                       |                                           |
| SQLITE\_MEMORY\_DATABASE\_NAME    | mormot.db.raw\.sqlite3               |                                           |
| StatusCodeIsSuccess               | mormot.core.os                       |                                           |
| StatusCodeToErrorMessage          | mormot.core.os                       | StatusCodeToReason                        |
| StringReplaceAll                  | mormot.core.text                     |                                           |
| StringToUTF8                      | mormot.core.unicode                  |                                           |
| SynSQLite3Static                  |                                      | mormot.db.raw\.sqlite3.static             |
| TAutoFree                         | mormot.core.data                     |                                           |
| TDocVariantData                   | mormot.core.variants                 |                                           |
| TDocVariantOption                 | mormot.core.data                     |                                           |
| TDynArray                         | mormot.core.data                     |                                           |
| TEchoWriter                       | mormot.core.text                     |                                           |
| TID                               | mormot.core.base                     |                                           |
| TimeLogToDateTime                 | mormot.core.datetime                 |                                           |
| TJSONToObjectOption               | mormot.core.json                     | TJsonParserOption                         |
| TModTime                          | mormot.orm.base                      |                                           |
| TNullable\*                       | mormot.db.core                       |                                           |
| ToClientDataSet                   | mormot.db.rad.ui.cds                 |                                           |
| TOleDB\*ConnectionProperties      | mormot.db.sql.oledb                  | TSqlDBOleDB\*ConnectionProperties         |
| TRawByteStringStream              | mormot.core.base                     |                                           |
| TRawUTF8List                      | mormot.core.data                     |                                           |
| Trim                              | mormot.core.base                     | TrimU                                     |
| TService                          | mormot.core.os                       |                                           |
| TSQLAccessRights                  | mormot.orm.core                      | TOrmAccessRights                          |
| TSQLDBConnection                  | mormot.db.sql                        |                                           |
| TSQLDBSQLite3ConnectionProperties | mormot.db.sql.sqlite3                |                                           |
| TSQLHTTPClient                    | mormot.rest.http.client              | TRestHTTPClient                           |
| TSQLHttpServer                    | mormot.rest.http.server              | TRestHttpServer                           |
| TSQLHttpServerSecurity            | mormot.rest.http.server              | TRestHttpServerSecurity                   |
| TSqlLockingMode                   | mormot.db.raw\.sqlite3               |                                           |
| TSQLLockingMode                   | mormot.db.raw\.sqlite3               |                                           |
| TSQLModel                         | mormot.orm.core                      | TOrmModel                                 |
| TSQLOccasion                      | mormot.orm.base                      | TOrmOccasion                              |
| TSQLRawBlob                       | mormot.core.base                     | RawBlob                                   |
| TSQLRecord                        | mormot.orm.core                      | TOrm                                      |
| TSQLRecordNoCase                  | mormot.orm.core                      | TOrmNoCase                                |
| TSQLRecordProperties              | mormot.orm.core                      | TOrmRecordProperties                      |
| TSQLRest                          | mormot.rest.core                     | TRest                                     |
| TSQLRestClientDB                  | mormot.rest.sqlite3                  | TRestClientDB                             |
| TSQLRestServer                    | mormot.rest.server                   | TRestServer                               |
| TSQLRestServerDB                  | mormot.rest.sqlite3                  | TRestServerDB                             |
| TSQLRestServerFullMemory          | mormot.rest.memserver                | TRestServerFullMemory                     |
| TSQLRestServerURIContext          | mormot.rest.server                   | TRestServerURIContext                     |
| TSQLSynchronousMode               | mormot.db.raw\.sqlite3               |                                           |
| TSQLTableJson                     | mormot.orm.core                      | TOrmTableJson                             |
| TSQLURIMethod                     | mormot.rest.core                     | TURIMethod                                |
| TSynBackgroundTimer               | mormot.core.threads                  |                                           |
| TSynDictionary                    | mormot.core.json                     |                                           |
| TSynFilter                        | mormot.core.search                   |                                           |
| TSynLocker                        | mormot.core.os                       |                                           |
| TSynLog                           | mormot.core.log                      |                                           |
| TSynLogInfo                       | mormot.core.base                     |                                           |
| TSynTimeZone                      | mormot.core.search                   |                                           |
| TTextWriterJsonFormat             | mormot.core.text                     |                                           |
| TURI                              | mormot.net.sock                      |                                           |
| TURIMethod                        | mormot.rest.core                     |                                           |
| TWinHTTP                          | mormot.net.client                    |                                           |
| UpdateIniNameValue                | mormot.core.data                     |                                           |
| UpperCase                         | mormot.core.unicode                  |                                           |
| UpperCaseUnicode                  | mormot.core.unicode                  |                                           |
| UrlDecode                         | mormot.core.buffers                  |                                           |
| UTF8ToString                      | mormot.core.unicode                  |                                           |
| VariantSaveJSON                   | mormot.core.text                     |                                           |
| VariantToDateTime                 | mormot.core.datetime                 |                                           |
| VariantToIntegerDef               | mormot.core.base                     |                                           |
| VariantToUTF8                     | mormot.core.text                     |                                           |
| VirtualTableExternalRegister      | mormot.orm.sql                       | OrmMapExternal                            |

**🌟 Output Directive:**

* Deliver the full project, including all `.pas` and `.dpr` files and the directory structure.
* Ensure each file is ready-to-compile, with explicit comments for each section.
* Present the response in blocks corresponding to each generation step, and wait for the user to reply with **"continue"** before proceeding to the next block.
