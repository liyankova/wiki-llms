---
url: https://bun.com/reference/bun/sqlite
title: bun:sqlite module | API Reference | Bun
source_domain: bun.com
---

# bun:sqlite module | API Reference | Bun

module

# [bun:sqlite](https://bun.com/reference/bun/sqlite)

The `'bun:sqlite'` module is a high-performance SQLite3 driver built directly into Bun. The API is simple, synchronous, and inspired by better-sqlite3, offering a clean and intuitive interface for database operations.

Key features include prepared statements, transactions, both named and positional parameters, datatype conversions (BLOB to Uint8Array), mapping query results to classes, and support for bigint. Multi-query statements can be executed in a single call to database.run().

Performance benchmarks show bun:sqlite is approximately 3-6x faster than better-sqlite3 and 8-9x faster than deno.land/x/sqlite for read queries, making it the fastest SQLite driver available for JavaScript.

* ### namespace [constants](https://bun.com/reference/bun/sqlite/constants)

  Constants from `sqlite3.h`

  This list isn't exhaustive, but some of the ones which are relevant

  + const [SQLITE\_FCNTL\_BEGIN\_ATOMIC\_WRITE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_BEGIN_ATOMIC_WRITE): number
  + const [SQLITE\_FCNTL\_BUSYHANDLER](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_BUSYHANDLER): number
  + const [SQLITE\_FCNTL\_CHUNK\_SIZE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_CHUNK_SIZE): number
  + const [SQLITE\_FCNTL\_CKPT\_DONE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_CKPT_DONE): number
  + const [SQLITE\_FCNTL\_CKPT\_START](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_CKPT_START): number
  + const [SQLITE\_FCNTL\_CKSM\_FILE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_CKSM_FILE): number
  + const [SQLITE\_FCNTL\_COMMIT\_ATOMIC\_WRITE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_COMMIT_ATOMIC_WRITE): number
  + const [SQLITE\_FCNTL\_COMMIT\_PHASETWO](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_COMMIT_PHASETWO): number
  + const [SQLITE\_FCNTL\_DATA\_VERSION](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_DATA_VERSION): number
  + const [SQLITE\_FCNTL\_EXTERNAL\_READER](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_EXTERNAL_READER): number
  + const [SQLITE\_FCNTL\_FILE\_POINTER](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_FILE_POINTER): number
  + const [SQLITE\_FCNTL\_GET\_LOCKPROXYFILE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_GET_LOCKPROXYFILE): number
  + const [SQLITE\_FCNTL\_HAS\_MOVED](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_HAS_MOVED): number
  + const [SQLITE\_FCNTL\_JOURNAL\_POINTER](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_JOURNAL_POINTER): number
  + const [SQLITE\_FCNTL\_LAST\_ERRNO](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_LAST_ERRNO): number
  + const [SQLITE\_FCNTL\_LOCK\_TIMEOUT](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_LOCK_TIMEOUT): number
  + const [SQLITE\_FCNTL\_LOCKSTATE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_LOCKSTATE): number
  + const [SQLITE\_FCNTL\_MMAP\_SIZE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_MMAP_SIZE): number
  + const [SQLITE\_FCNTL\_OVERWRITE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_OVERWRITE): number
  + const [SQLITE\_FCNTL\_PDB](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_PDB): number
  + const [SQLITE\_FCNTL\_PERSIST\_WAL](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_PERSIST_WAL): number
  + const [SQLITE\_FCNTL\_POWERSAFE\_OVERWRITE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_POWERSAFE_OVERWRITE): number
  + const [SQLITE\_FCNTL\_PRAGMA](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_PRAGMA): number
  + const [SQLITE\_FCNTL\_RBU](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_RBU): number
  + const [SQLITE\_FCNTL\_RESERVE\_BYTES](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_RESERVE_BYTES): number
  + const [SQLITE\_FCNTL\_RESET\_CACHE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_RESET_CACHE): number
  + const [SQLITE\_FCNTL\_ROLLBACK\_ATOMIC\_WRITE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_ROLLBACK_ATOMIC_WRITE): number
  + const [SQLITE\_FCNTL\_SET\_LOCKPROXYFILE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_SET_LOCKPROXYFILE): number
  + const [SQLITE\_FCNTL\_SIZE\_HINT](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_SIZE_HINT): number
  + const [SQLITE\_FCNTL\_SIZE\_LIMIT](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_SIZE_LIMIT): number
  + const [SQLITE\_FCNTL\_SYNC](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_SYNC): number
  + const [SQLITE\_FCNTL\_SYNC\_OMITTED](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_SYNC_OMITTED): number
  + const [SQLITE\_FCNTL\_TEMPFILENAME](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_TEMPFILENAME): number
  + const [SQLITE\_FCNTL\_TRACE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_TRACE): number
  + const [SQLITE\_FCNTL\_VFS\_POINTER](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_VFS_POINTER): number
  + const [SQLITE\_FCNTL\_VFSNAME](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_VFSNAME): number
  + const [SQLITE\_FCNTL\_WAL\_BLOCK](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_WAL_BLOCK): number
  + const [SQLITE\_FCNTL\_WIN32\_AV\_RETRY](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_WIN32_AV_RETRY): number
  + const [SQLITE\_FCNTL\_WIN32\_GET\_HANDLE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_WIN32_GET_HANDLE): number
  + const [SQLITE\_FCNTL\_WIN32\_SET\_HANDLE](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_WIN32_SET_HANDLE): number
  + const [SQLITE\_FCNTL\_ZIPVFS](https://bun.com/reference/bun/sqlite/constants/SQLITE_FCNTL_ZIPVFS): number
  + const [SQLITE\_OPEN\_AUTOPROXY](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_AUTOPROXY): number
  + const [SQLITE\_OPEN\_CREATE](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_CREATE): number

    Allow creating a new database
  + const [SQLITE\_OPEN\_DELETEONCLOSE](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_DELETEONCLOSE): number
  + const [SQLITE\_OPEN\_EXCLUSIVE](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_EXCLUSIVE): number
  + const [SQLITE\_OPEN\_EXRESCODE](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_EXRESCODE): number
  + const [SQLITE\_OPEN\_FULLMUTEX](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_FULLMUTEX): number
  + const [SQLITE\_OPEN\_MAIN\_DB](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_MAIN_DB): number
  + const [SQLITE\_OPEN\_MAIN\_JOURNAL](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_MAIN_JOURNAL): number
  + const [SQLITE\_OPEN\_MEMORY](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_MEMORY): number
  + const [SQLITE\_OPEN\_NOFOLLOW](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_NOFOLLOW): number
  + const [SQLITE\_OPEN\_NOMUTEX](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_NOMUTEX): number
  + const [SQLITE\_OPEN\_PRIVATECACHE](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_PRIVATECACHE): number
  + const [SQLITE\_OPEN\_READONLY](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_READONLY): number

    Open the database as read-only (no write operations, no create).
  + const [SQLITE\_OPEN\_READWRITE](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_READWRITE): number

    Open the database for reading and writing
  + const [SQLITE\_OPEN\_SHAREDCACHE](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_SHAREDCACHE): number
  + const [SQLITE\_OPEN\_SUBJOURNAL](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_SUBJOURNAL): number
  + const [SQLITE\_OPEN\_SUPER\_JOURNAL](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_SUPER_JOURNAL): number
  + const [SQLITE\_OPEN\_TEMP\_DB](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_TEMP_DB): number
  + const [SQLITE\_OPEN\_TEMP\_JOURNAL](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_TEMP_JOURNAL): number
  + const [SQLITE\_OPEN\_TRANSIENT\_DB](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_TRANSIENT_DB): number
  + const [SQLITE\_OPEN\_URI](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_URI): number
  + const [SQLITE\_OPEN\_WAL](https://bun.com/reference/bun/sqlite/constants/SQLITE_OPEN_WAL): number
  + const [SQLITE\_PREPARE\_NO\_VTAB](https://bun.com/reference/bun/sqlite/constants/SQLITE_PREPARE_NO_VTAB): number
  + const [SQLITE\_PREPARE\_NORMALIZE](https://bun.com/reference/bun/sqlite/constants/SQLITE_PREPARE_NORMALIZE): number
  + const [SQLITE\_PREPARE\_PERSISTENT](https://bun.com/reference/bun/sqlite/constants/SQLITE_PREPARE_PERSISTENT): number
* ### class [Database](https://bun.com/reference/bun/sqlite/Database)

  A SQLite3 database

  ```
  const db = new Database("mydb.sqlite");
  db.run("CREATE TABLE foo (bar TEXT)");
  db.run("INSERT INTO foo VALUES (?)", ["baz"]);
  console.log(db.query("SELECT * FROM foo").all());
  ```

  + readonly [filename](https://bun.com/reference/bun/sqlite/Database/filename): string

    The filename passed when `new Database()` was called

    ```
    const db = new Database("mydb.sqlite");
    console.log(db.filename);
    // => "mydb.sqlite"
    ```
  + readonly [handle](https://bun.com/reference/bun/sqlite/Database/handle): number

    The underlying `sqlite3` database handle

    In native code, this is not a file descriptor, but an index into an array of database handles
  + [[Symbol.dispose]](https://bun.com/reference/bun/sqlite/Database/[dispose])(): void;

    Closes the database when using the async resource proposal

    ```
    using db = new Database("myapp.db");
    doSomethingWithDatabase(db);
    // Automatically closed when `db` goes out of scope
    ```
  + [close](https://bun.com/reference/bun/sqlite/Database/close)(

    throwOnError?: boolean

    ): void;

    Close the database connection.

    It is safe to call this method multiple times. If the database is already closed, this is a no-op. Running queries after the database has been closed will throw an error.

    @param throwOnError

    If `true`, then the database will throw an error if it is in use

    ```
    db.close();
    ```

    This is called automatically when the database instance is garbage collected.

    Internally, this calls `sqlite3_close_v2`.
  + [fileControl](https://bun.com/reference/bun/sqlite/Database/fileControl)(

    op: number,

    arg?: number | ArrayBufferView<ArrayBufferLike>

    ): number;

    See `sqlite3_file_control` for more information.

    [fileControl](https://bun.com/reference/bun/sqlite/Database/fileControl)(

    zDbName: string,

    op: number,

    arg?: number | ArrayBufferView<ArrayBufferLike>

    ): number;

    See `sqlite3_file_control` for more information.
  + [loadExtension](https://bun.com/reference/bun/sqlite/Database/loadExtension)(

    extension: string,

    entryPoint?: string

    ): void;

    Load a SQLite3 extension

    macOS requires a custom SQLite3 library to be linked because the Apple build of SQLite for macOS disables loading extensions. See Database.setCustomSQLite

    Bun chooses the Apple build of SQLite on macOS because it brings a ~50% performance improvement.

    @param extension

    name/path of the extension to load

    @param entryPoint

    optional entry point of the extension
  + [prepare](https://bun.com/reference/bun/sqlite/Database/prepare)<ReturnType, ParamsType extends [SQLQueryBindings](https://bun.com/reference/bun/sqlite/SQLQueryBindings) | [SQLQueryBindings](https://bun.com/reference/bun/sqlite/SQLQueryBindings)[]>(

    sql: string,

    params?: ParamsType

    ): [Statement](https://bun.com/reference/bun/sqlite/Statement)<ReturnType, ParamsType extends any[] ? ParamsType<ParamsType> : [ParamsType]>;

    Compile a SQL query and return a Statement object.

    This does not cache the compiled query and does not execute the query.

    Under the hood, this calls `sqlite3_prepare_v3`.

    @param sql

    The SQL query to compile

    @param params

    Optional bindings for the query

    @returns

    A Statement instance

    ```
    // compile the query
    const stmt = db.query("SELECT * FROM foo WHERE bar = ?");
    // run the query
    stmt.all("baz");
    ```
  + [query](https://bun.com/reference/bun/sqlite/Database/query)<ReturnType, ParamsType extends [SQLQueryBindings](https://bun.com/reference/bun/sqlite/SQLQueryBindings) | [SQLQueryBindings](https://bun.com/reference/bun/sqlite/SQLQueryBindings)[]>(

    sql: string

    ): [Statement](https://bun.com/reference/bun/sqlite/Statement)<ReturnType, ParamsType extends any[] ? ParamsType<ParamsType> : [ParamsType]>;

    Compile a SQL query and return a Statement object. This is the same as prepare except that it caches the compiled query.

    This **does not execute** the query, but instead prepares it for later execution and caches the compiled query if possible.

    Under the hood, this calls `sqlite3_prepare_v3`.

    @param sql

    The SQL query to compile

    @returns

    `Statment` instance

    ```
    // compile the query
    const stmt = db.query("SELECT * FROM foo WHERE bar = ?");
    // run the query
    stmt.all("baz");

    // run the query again
    stmt.all();
    ```
  + [run](https://bun.com/reference/bun/sqlite/Database/run)<ParamsType extends [SQLQueryBindings](https://bun.com/reference/bun/sqlite/SQLQueryBindings)[]>(

    sql: string,

    ...bindings: ParamsType[]

    ): [Changes](https://bun.com/reference/bun/sqlite/Changes);

    Execute a SQL query **without returning any results**.

    This does not cache the query, so if you want to run a query multiple times, you should use prepare instead.

    Under the hood, this calls `sqlite3_prepare_v3` followed by `sqlite3_step` and `sqlite3_finalize`.

    The following types can be used when binding parameters:

    | JavaScript type | SQLite type |
    | --- | --- |
    | `string` | `TEXT` |
    | `number` | `INTEGER` or `DECIMAL` |
    | `boolean` | `INTEGER` (1 or 0) |
    | `Uint8Array` | `BLOB` |
    | `Buffer` | `BLOB` |
    | `bigint` | `INTEGER` |
    | `null` | `NULL` |

    @param sql

    The SQL query to run

    @param bindings

    Optional bindings for the query

    @returns

    `Database` instance

    ```
    db.run("CREATE TABLE foo (bar TEXT)");
    db.run("INSERT INTO foo VALUES (?)", ["baz"]);
    ```

    Useful for queries like:

    - `CREATE TABLE`
    - `INSERT INTO`
    - `UPDATE`
    - `DELETE FROM`
    - `DROP TABLE`
    - `PRAGMA`
    - `ATTACH DATABASE`
    - `DETACH DATABASE`
    - `REINDEX`
    - `VACUUM`
    - `EXPLAIN ANALYZE`
    - `CREATE INDEX`
    - `CREATE TRIGGER`
    - `CREATE VIEW`
    - `CREATE VIRTUAL TABLE`
    - `CREATE TEMPORARY TABLE`
  + [serialize](https://bun.com/reference/bun/sqlite/Database/serialize)(

    name?: string

    ): [Buffer](https://bun.com/reference/node/buffer/Buffer);

    Save the database to an in-memory Buffer object.

    Internally, this calls `sqlite3_serialize`.

    @param name

    Name to save the database as

    @returns

    Buffer containing the serialized database
  + [transaction](https://bun.com/reference/bun/sqlite/Database/transaction)<A extends any[], T>(

    insideTransaction: (...args: A) => T

    ): (...args: A) => T;

    Creates a function that always runs inside a transaction. When the function is invoked, it will begin a new transaction. When the function returns, the transaction will be committed. If an exception is thrown, the transaction will be rolled back (and the exception will propagate as usual).

    @param insideTransaction

    The callback which runs inside a transaction

    ```
    // setup
    import { Database } from "bun:sqlite";
    const db = Database.open(":memory:");
    db.exec(
      "CREATE TABLE cats (id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT UNIQUE, age INTEGER)"
    );

    const insert = db.prepare("INSERT INTO cats (name, age) VALUES ($name, $age)");
    const insertMany = db.transaction((cats) => {
      for (const cat of cats) insert.run(cat);
    });

    insertMany([
      { $name: "Joey", $age: 2 },
      { $name: "Sally", $age: 4 },
      { $name: "Junior", $age: 1 },
    ]);
    ```
  + static [deserialize](https://bun.com/reference/bun/sqlite/Database/deserialize)(

    serialized: ArrayBufferLike | TypedArray<ArrayBufferLike>,

    isReadOnly?: boolean

    ): [Database](https://bun.com/reference/bun/sqlite/Database);

    Load a serialized SQLite3 database

    Internally, this calls `sqlite3_deserialize`.

    @param serialized

    Data to load

    @returns

    `Database` instance

    ```
    test("supports serialize/deserialize", () => {
        const db = Database.open(":memory:");
        db.exec("CREATE TABLE test (id INTEGER PRIMARY KEY, name TEXT)");
        db.exec('INSERT INTO test (name) VALUES ("Hello")');
        db.exec('INSERT INTO test (name) VALUES ("World")');

        const input = db.serialize();
        const db2 = new Database(input);

        const stmt = db2.prepare("SELECT * FROM test");
        expect(JSON.stringify(stmt.get())).toBe(
          JSON.stringify({
            id: 1,
            name: "Hello",
          }),
        );

        expect(JSON.stringify(stmt.all())).toBe(
          JSON.stringify([
            {
              id: 1,
              name: "Hello",
            },
            {
              id: 2,
              name: "World",
            },
          ]),
        );
        db2.exec("insert into test (name) values ('foo')");
        expect(JSON.stringify(stmt.all())).toBe(
          JSON.stringify([
            {
              id: 1,
              name: "Hello",
            },
            {
              id: 2,
              name: "World",
            },
            {
              id: 3,
              name: "foo",
            },
          ]),
        );

        const db3 = Database.deserialize(input, true);
        try {
          db3.exec("insert into test (name) values ('foo')");
          throw new Error("Expected error");
        } catch (e) {
          expect(e.message).toBe("attempt to write a readonly database");
        }
    });
    ```

    static [deserialize](https://bun.com/reference/bun/sqlite/Database/deserialize)(

    serialized: ArrayBufferLike | TypedArray<ArrayBufferLike>,

    options?: { readonly: boolean; safeIntegers: boolean; strict: boolean }

    ): [Database](https://bun.com/reference/bun/sqlite/Database);

    Load a serialized SQLite3 database. This version enables you to specify additional options such as `strict` to put the database into strict mode.

    Internally, this calls `sqlite3_deserialize`.

    @param serialized

    Data to load

    @returns

    `Database` instance

    ```
    test("supports serialize/deserialize", () => {
        const db = Database.open(":memory:");
        db.exec("CREATE TABLE test (id INTEGER PRIMARY KEY, name TEXT)");
        db.exec('INSERT INTO test (name) VALUES ("Hello")');
        db.exec('INSERT INTO test (name) VALUES ("World")');

        const input = db.serialize();
        const db2 = Database.deserialize(input, { strict: true });

        const stmt = db2.prepare("SELECT * FROM test");
        expect(JSON.stringify(stmt.get())).toBe(
          JSON.stringify({
            id: 1,
            name: "Hello",
          }),
        );

        expect(JSON.stringify(stmt.all())).toBe(
          JSON.stringify([
            {
              id: 1,
              name: "Hello",
            },
            {
              id: 2,
              name: "World",
            },
          ]),
        );
        db2.exec("insert into test (name) values ($foo)", { foo: "baz" });
        expect(JSON.stringify(stmt.all())).toBe(
          JSON.stringify([
            {
              id: 1,
              name: "Hello",
            },
            {
              id: 2,
              name: "World",
            },
            {
              id: 3,
              name: "baz",
            },
          ]),
        );

        const db3 = Database.deserialize(input, { readonly: true, strict: true });
        try {
          db3.exec("insert into test (name) values ($foo)", { foo: "baz" });
          throw new Error("Expected error");
        } catch (e) {
          expect(e.message).toBe("attempt to write a readonly database");
        }
    });
    ```
  + static [open](https://bun.com/reference/bun/sqlite/Database/open)(

    filename: string,

    options?: number | [DatabaseOptions](https://bun.com/reference/bun/sqlite/DatabaseOptions)

    ): [Database](https://bun.com/reference/bun/sqlite/Database);

    Open or create a SQLite3 databases

    @param filename

    The filename of the database to open. Pass an empty string (`""`) or `":memory:"` or undefined for an in-memory database.

    @param options

    defaults to `{readwrite: true, create: true}`. If a number, then it's treated as `SQLITE_OPEN_*` constant flags.

    This is an alias of `new Database()`

    See Database
  + static [setCustomSQLite](https://bun.com/reference/bun/sqlite/Database/setCustomSQLite)(

    path: string

    ): boolean;

    Change the dynamic library path to SQLite

    @param path

    The path to the SQLite library
* ### class [SQLiteError](https://bun.com/reference/bun/sqlite/SQLiteError)

  Errors from SQLite have a name `SQLiteError`.

  + readonly [byteOffset](https://bun.com/reference/bun/sqlite/SQLiteError/byteOffset): number

    The UTF-8 byte offset of the sqlite3 query that failed, if known

    This corresponds to `sqlite3_error_offset`.
  + [cause](https://bun.com/reference/bun/sqlite/SQLiteError/cause)?: unknown

    The cause of the error.
  + [code](https://bun.com/reference/bun/sqlite/SQLiteError/code)?: string

    The name of the SQLite3 error code

    ```
    "SQLITE_CONSTRAINT_UNIQUE"
    ```
  + [errno](https://bun.com/reference/bun/sqlite/SQLiteError/errno): number

    The SQLite3 extended error code

    This corresponds to `sqlite3_extended_errcode`.
  + [message](https://bun.com/reference/bun/sqlite/SQLiteError/message): string
  + readonly [name](https://bun.com/reference/bun/sqlite/SQLiteError/name): 'SQLiteError'
  + [stack](https://bun.com/reference/bun/sqlite/SQLiteError/stack)?: string
  + static [stackTraceLimit](https://bun.com/reference/bun/sqlite/SQLiteError/stackTraceLimit): number

    The `Error.stackTraceLimit` property specifies the number of stack frames collected by a stack trace (whether generated by `new Error().stack` or `Error.captureStackTrace(obj)`).

    The default value is `10` but may be set to any valid JavaScript number. Changes will affect any stack trace captured *after* the value has been changed.

    If set to a non-number value, or set to a negative number, stack traces will not capture any frames.
  + static [captureStackTrace](https://bun.com/reference/bun/sqlite/SQLiteError/captureStackTrace)(

    targetObject: object,

    constructorOpt?: Function

    ): void;

    Create .stack property on a target object
  + static [isError](https://bun.com/reference/bun/sqlite/SQLiteError/isError)(

    value: unknown

    ): value is [Error](https://bun.com/reference/globals/Error);

    Check if a value is an instance of Error

    @param value

    The value to check

    @returns

    True if the value is an instance of Error, false otherwise
  + static [prepareStackTrace](https://bun.com/reference/bun/sqlite/SQLiteError/prepareStackTrace)(

    err: [Error](https://bun.com/reference/globals/Error),

    stackTraces: CallSite[]

    ): any;
* ### class [Statement](https://bun.com/reference/bun/sqlite/Statement)<ReturnType = unknown, ParamsType extends [SQLQueryBindings](https://bun.com/reference/bun/sqlite/SQLQueryBindings)[] = any[]>

  A prepared statement.

  This is returned by Database.prepare and Database.query.

  ```
  const stmt = db.prepare("SELECT * FROM foo WHERE bar = ?");
  stmt.all("baz");
  // => [{bar: "baz"}]
  ```

  + readonly [columnNames](https://bun.com/reference/bun/sqlite/Statement/columnNames): string[]

    The names of the columns returned by the prepared statement.

    ```
    const stmt = db.prepare("SELECT bar FROM foo WHERE bar = ?");

    console.log(stmt.columnNames);
    // => ["bar"]
    ```
  + readonly [columnTypes](https://bun.com/reference/bun/sqlite/Statement/columnTypes): null | 'TEXT' | 'INTEGER' | 'FLOAT' | 'BLOB' | 'NULL'[]

    The actual SQLite column types from the first row of the result set. Useful for expressions and computed columns, which are not covered by `declaredTypes`

    Returns an array of SQLite type constants as uppercase strings:

    - `"INTEGER"` for integer values
    - `"FLOAT"` for floating-point values
    - `"TEXT"` for text values
    - `"BLOB"` for binary data
    - `"NULL"` for null values
    - `null` for unknown/unsupported types

    **Requirements:**

    - Only available for read-only statements (SELECT queries)
    - For non-read-only statements, throws an error

    **Behavior:**

    - Uses `sqlite3_column_type()` to get actual data types from the first row
    - Returns `null` for columns with unknown SQLite type constants

    ```
    const stmt = db.prepare("SELECT id, name, age FROM users WHERE id = 1");

    console.log(stmt.columnTypes);
    // => ["INTEGER", "TEXT", "INTEGER"]

    // For expressions:
    const exprStmt = db.prepare("SELECT length('bun') AS str_length");
    console.log(exprStmt.columnTypes);
    // => ["INTEGER"]
    ```
  + readonly [declaredTypes](https://bun.com/reference/bun/sqlite/Statement/declaredTypes): null | string[]

    The declared column types from the table schema.

    Returns an array of declared type strings from `sqlite3_column_decltype()`:

    - Raw type strings as declared in the CREATE TABLE statement
    - `null` for columns without declared types (e.g., expressions, computed columns)

    **Requirements:**

    - Statement must be executed at least once before accessing this property
    - Available for both read-only and read-write statements

    **Behavior:**

    - Uses `sqlite3_column_decltype()` to get schema-declared types
    - Returns the exact type string from the table definition

    ```
    // For table columns:
    const stmt = db.prepare("SELECT id, name, weight FROM products");
    stmt.get();
    console.log(stmt.declaredTypes);
    // => ["INTEGER", "TEXT", "REAL"]

    // For expressions (no declared types):
    const exprStmt = db.prepare("SELECT length('bun') AS str_length");
    exprStmt.get();
    console.log(exprStmt.declaredTypes);
    // => [null]
    ```
  + readonly [native](https://bun.com/reference/bun/sqlite/Statement/native): any

    Native object representing the underlying `sqlite3_stmt`

    This is left untyped because the ABI of the native bindings may change at any time.

    For stable, typed access to statement metadata, use the typed properties on the Statement class:

    - columnNames for column names
    - paramsCount for parameter count
    - columnTypes for actual data types from the first row
    - declaredTypes for schema-declared column types
  + readonly [paramsCount](https://bun.com/reference/bun/sqlite/Statement/paramsCount): number

    The number of parameters expected in the prepared statement.

    ```
    const stmt = db.prepare("SELECT * FROM foo WHERE bar = ?");
    console.log(stmt.paramsCount);
    // => 1
    ```
  + [[Symbol.dispose]](https://bun.com/reference/bun/sqlite/Statement/[dispose])(): void;

    Calls finalize if it wasn't already called.
  + [[Symbol.iterator]](https://bun.com/reference/bun/sqlite/Statement/[iterator])(): IterableIterator<ReturnType>;
  + [all](https://bun.com/reference/bun/sqlite/Statement/all)(

    ...params: ParamsType

    ): ReturnType[];

    Execute the prepared statement and return all results as objects.

    @param params

    optional values to bind to the statement. If omitted, the statement is run with the last bound values or no parameters if there are none.

    ```
    const stmt = db.prepare("SELECT * FROM foo WHERE bar = ?");

    stmt.all("baz");
    // => [{bar: "baz"}]

    stmt.all();
    // => []

    stmt.all("foo");
    // => [{bar: "foo"}]
    ```
  + [as](https://bun.com/reference/bun/sqlite/Statement/as)<T = unknown>(

    Class: new (...args: any[]) => T

    ): [Statement](https://bun.com/reference/bun/sqlite/Statement)<T, ParamsType>;

    Make get and all return an instance of the provided `Class` instead of the default `Object`.

    @param Class

    A class to use

    @returns

    The same statement instance, modified to return an instance of `Class`

    This lets you attach methods, getters, and setters to the returned objects.

    For performance reasons, constructors for classes are not called, which means initializers will not be called and private fields will not be accessible.

    ## [Custom class](https://bun.com/reference/bun/sqlite#custom-class)

    ```
    class User {
       rawBirthdate: string;
       get birthdate() {
         return new Date(this.rawBirthdate);
       }
    }

    const db = new Database(":memory:");
    db.exec("CREATE TABLE users (id INTEGER PRIMARY KEY, rawBirthdate TEXT)");
    db.run("INSERT INTO users (rawBirthdate) VALUES ('1995-12-19')");
    const query = db.query("SELECT * FROM users");
    query.as(User);
    const user = query.get();
    console.log(user.birthdate);
    // => Date(1995, 12, 19)
    ```
  + [finalize](https://bun.com/reference/bun/sqlite/Statement/finalize)(): void;

    Finalize the prepared statement, freeing the resources used by the statement and preventing it from being executed again.

    This is called automatically when the prepared statement is garbage collected.

    It is safe to call this multiple times. Calling this on a finalized statement has no effect.

    Internally, this calls `sqlite3_finalize`.
  + [get](https://bun.com/reference/bun/sqlite/Statement/get)(

    ...params: ParamsType

    ): null | ReturnType;

    Execute the prepared statement and return **the first** result.

    If no result is returned, this returns `null`.

    @param params

    optional values to bind to the statement. If omitted, the statement is run with the last bound values or no parameters if there are none.

    ```
    const stmt = db.prepare("SELECT * FROM foo WHERE bar = ?");

    stmt.get("baz");
    // => {bar: "baz"}

    stmt.get();
    // => null

    stmt.get("foo");
    // => {bar: "foo"}
    ```

    The following types can be used when binding parameters:

    | JavaScript type | SQLite type |
    | --- | --- |
    | `string` | `TEXT` |
    | `number` | `INTEGER` or `DECIMAL` |
    | `boolean` | `INTEGER` (1 or 0) |
    | `Uint8Array` | `BLOB` |
    | `Buffer` | `BLOB` |
    | `bigint` | `INTEGER` |
    | `null` | `NULL` |
  + [iterate](https://bun.com/reference/bun/sqlite/Statement/iterate)(

    ...params: ParamsType

    ): IterableIterator<ReturnType>;

    Execute the prepared statement and return an

    @param params

    optional values to bind to the statement. If omitted, the statement is run with the last bound values or no parameters if there are none.
  + [raw](https://bun.com/reference/bun/sqlite/Statement/raw)(

    ...params: ParamsType

    ): null | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>[][];

    Execute the prepared statement and return all results as arrays of `Uint8Array`s.

    This is similar to `values()` but returns all values as Uint8Array objects, regardless of their original SQLite type.

    @param params

    optional values to bind to the statement. If omitted, the statement is run with the last bound values or no parameters if there are none.

    ```
    const stmt = db.prepare("SELECT * FROM foo WHERE bar = ?");

    stmt.raw("baz");
    // => [[Uint8Array(24)]]

    stmt.raw();
    // => [[Uint8Array(24)]]
    ```
  + [run](https://bun.com/reference/bun/sqlite/Statement/run)(

    ...params: ParamsType

    ): [Changes](https://bun.com/reference/bun/sqlite/Changes);

    Execute the prepared statement.

    @param params

    optional values to bind to the statement. If omitted, the statement is run with the last bound values or no parameters if there are none.

    ```
    const stmt = db.prepare("UPDATE foo SET bar = ?");
    stmt.run("baz");
    // => undefined

    stmt.run();
    // => undefined

    stmt.run("foo");
    // => undefined
    ```

    The following types can be used when binding parameters:

    | JavaScript type | SQLite type |
    | --- | --- |
    | `string` | `TEXT` |
    | `number` | `INTEGER` or `DECIMAL` |
    | `boolean` | `INTEGER` (1 or 0) |
    | `Uint8Array` | `BLOB` |
    | `Buffer` | `BLOB` |
    | `bigint` | `INTEGER` |
    | `null` | `NULL` |
  + [toString](https://bun.com/reference/bun/sqlite/Statement/toString)(): string;

    Return the expanded SQL string for the prepared statement.

    Internally, this calls `sqlite3_expanded_sql()` on the underlying `sqlite3_stmt`.

    ```
    const stmt = db.prepare("SELECT * FROM foo WHERE bar = ?", "baz");
    console.log(stmt.toString());
    // => "SELECT * FROM foo WHERE bar = 'baz'"
    console.log(stmt);
    // => "SELECT * FROM foo WHERE bar = 'baz'"
    ```
  + [values](https://bun.com/reference/bun/sqlite/Statement/values)(

    ...params: ParamsType

    ): string | number | bigint | boolean | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>[][];

    Execute the prepared statement and return the results as an array of arrays.

    In Bun v0.6.7 and earlier, this method returned `null` if there were no results instead of `[]`. This was changed in v0.6.8 to align more with what people expect.

    @param params

    optional values to bind to the statement. If omitted, the statement is run with the last bound values or no parameters if there are none.

    ```
    const stmt = db.prepare("SELECT * FROM foo WHERE bar = ?");

    stmt.values("baz");
    // => [['baz']]

    stmt.values();
    // => [['baz']]

    stmt.values("foo");
    // => [['foo']]

    stmt.values("not-found");
    // => []
    ```

    The following types can be used when binding parameters:

    | JavaScript type | SQLite type |
    | --- | --- |
    | `string` | `TEXT` |
    | `number` | `INTEGER` or `DECIMAL` |
    | `boolean` | `INTEGER` (1 or 0) |
    | `Uint8Array` | `BLOB` |
    | `Buffer` | `BLOB` |
    | `bigint` | `INTEGER` |
    | `null` | `NULL` |
* const [native](https://bun.com/reference/bun/sqlite/native): any

  The native module implementing the sqlite3 C bindings

  It is lazily-initialized, so this will return `undefined` until the first call to new Database().

  The native module makes no gurantees about ABI stability, so it is left untyped

  If you need to use it directly for some reason, please let us know because that probably points to a deficiency in this API.

## Type definitions

* ### interface [Changes](https://bun.com/reference/bun/sqlite/Changes)

  An object representing the changes made to the database since the last `run` or `exec` call.

  + [changes](https://bun.com/reference/bun/sqlite/Changes/changes): number

    The number of rows changed by the last `run` or `exec` call.
  + [lastInsertRowid](https://bun.com/reference/bun/sqlite/Changes/lastInsertRowid): number | bigint

    If `safeIntegers` is `true`, this is a `bigint`. Otherwise, it is a `number`.
* ### interface [DatabaseOptions](https://bun.com/reference/bun/sqlite/DatabaseOptions)

  Options for Database

  + [create](https://bun.com/reference/bun/sqlite/DatabaseOptions/create)?: boolean

    Allow creating a new database

    Equivalent to constants.SQLITE\_OPEN\_CREATE
  + [readonly](https://bun.com/reference/bun/sqlite/DatabaseOptions/readonly)?: boolean

    Open the database as read-only (no write operations, no create).

    Equivalent to constants.SQLITE\_OPEN\_READONLY
  + [readwrite](https://bun.com/reference/bun/sqlite/DatabaseOptions/readwrite)?: boolean

    Open the database as read-write

    Equivalent to constants.SQLITE\_OPEN\_READWRITE
  + [safeIntegers](https://bun.com/reference/bun/sqlite/DatabaseOptions/safeIntegers)?: boolean

    When set to `true`, integers are returned as `bigint` types.

    When set to `false`, integers are returned as `number` types and truncated to 52 bits.
  + [strict](https://bun.com/reference/bun/sqlite/DatabaseOptions/strict)?: boolean

    When set to `false` or `undefined`:

    - Queries missing bound parameters will NOT throw an error
    - Bound named parameters in JavaScript need to exactly match the SQL query.

    ```
    const db = new Database(":memory:", { strict: false });
    db.run("INSERT INTO foo (name) VALUES ($name)", { $name: "foo" });
    ```

    When set to `true`:

    - Queries missing bound parameters will throw an error
    - Bound named parameters in JavaScript no longer need to be `$`, `:`, or `@`. The SQL query will remain prefixed.
* type [SQLQueryBindings](https://bun.com/reference/bun/sqlite/SQLQueryBindings) = string | bigint | NodeJS.TypedArray | number | boolean | null | Record<string, string | bigint | NodeJS.TypedArray | number | boolean | null>