## Create DB Class
```
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class Db {
  Database? db;

  Future<Database> getDatabase() async {
    if(db==null) {
      String path = await getDatabasesPath();
      db =  await openDatabase(join(path, '$DBNAME$.db'),
          onCreate: (db, version) async {
        // CREATE TABLES HERE
          }, version: 1); 
    }
    
    return db!;
  }

}
```

## Create new CRUD with sqflite
```
static const String table$TABLENAME$ = 'table$TABLENAME$';
static const String m$TABLENAME$ColumnId = 'id';

Future<void> createTable(Database db) async {
  await db.execute('''
    CREATE TABLE table$TABLENAME$ (
      $$m$TABLENAME$ColumnId INTEGER PRIMARY KEY AUTOINCREMENT,
      $COLUMNS$
    )
  ''');
}

Future<int> insert$TABLENAME$(Map<String, dynamic> data) async {
  final db = await getDatabase();
  return await db.insert(
    table$TABLENAME$,
    data,
    conflictAlgorithm: ConflictAlgorithm.replace,
  );
}

Future<int> update$TABLENAME$(Map<String, dynamic> data) async {
  final db = await getDatabase();
  return await db.update(
    table$TABLENAME$,
    data,
    where: '$$m$TABLENAME$ColumnId = ?',
    whereArgs: [data[m$TABLENAME$ColumnId]],
  );
}

Future<int> delete$TABLENAME$(int id) async {
  final db = await getDatabase();
  return await db.delete(
    table$TABLENAME$,
    where: '$$m$TABLENAME$ColumnId = ?',
    whereArgs: [id],
  );
}

Future<List<Map<String, dynamic>>> getAll$TABLENAME$() async {
  final db = await getDatabase();
  final List<Map<String, dynamic>> maps = await db.query(table$TABLENAME$);
  return maps;
}

Future<Map<String, dynamic>?> get$TABLENAME$ById(int id) async {
  final db = await getDatabase();
  final List<Map<String, dynamic>> maps = await db.query(
    table$TABLENAME$,
    where: '$$m$TABLENAME$ColumnId = ?',
    whereArgs: [id],
  );
  if (maps.isNotEmpty) {
    return maps.first;
  }
  return null;
}

```

## Add PostFrame Callback
```
WidgetsBinding.instance.addPostFrameCallback((_) {
  $ACTION$
});
```

## GET & PUT Boolean Preference
```
static const m$propertyName$ = '$propertyName$';

static Future<bool?> get$propertyName$() async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getBool(m$propertyName$);
}

static Future<void> set$propertyName$(bool value) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setBool(m$propertyName$, value);
}
```

## GET & PUT Int Preference
```
static const m$propertyName$ = '$propertyName$';

static Future<double?> get$propertyName$() async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getDouble(m$propertyName$);
}

static Future<void> set$propertyName$(double value) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setDouble(m$propertyName$, value);
}
```

## GET & PUT Double Preference
```
static const m$propertyName$ = '$propertyName$';

static Future<int?> get$propertyName$() async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getInt(m$propertyName$);
}

static Future<void> set$propertyName$(int value) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setInt(m$propertyName$, value);
}
```

## GET & PUT String Preference
```
static const m$propertyName$ = '$propertyName$';

static Future<String?> get$propertyName$() async {
    final prefs = await SharedPreferences.getInstance();
    return prefs.getString(m$propertyName$);
}

static Future<void> set$propertyName$(String value) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setString(m$propertyName$, value);
}
```

## Try Catch
```
try {
  $TRYACTION$
}catch(e) {
  $CATCHACTION$
  if(kDebugMode) {
    print(e.toString());
  }
}
```

## ARB Text For Localization
```
"$TITLE$": "$TEXT$",
"@$TITLE$": {
    "description": "$DESCCRIPTION$"
}
```

## For Loop a List Indexed
```
for(int i=0; i<$LIST$.length; i++) {
  $ACTION$
}
```