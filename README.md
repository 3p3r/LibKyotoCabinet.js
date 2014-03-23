LibKyotoCabinet.js
==================

***Kyoto Cabinet, cross compiled to JavaScript, no C modules no dependencies!***

> Kyoto Cabinet is a library of routines for managing a database. The database is a simple data file containing records, each is a pair of a key and a value. Every key and value is serial bytes with variable length. Both binary data and character string can be used as a key and a value. Each key must be unique within a database. There is neither concept of data tables nor data types. Records are organized in hash table or B+ tree.

Original Kyoto Cabinet is GNU licensed. LibKyotoCabinet.js is MIT licensed.

Usage
-----
    //include libkyotocabinet.js
    //Wrap your desired C api's from the original library like:
    
    kcdbnew = Module.cwrap('kcdbnew');
    kcdbopen = Module.cwrap('kcdbopen','number',['number','string','number']);
    kcdbset = Module.cwrap('kcdbset','number',['number','string','number','string','number']);
    kcdbget = Module.cwrap('kcdbget','string',['number','string','number','number']);
    kcecodename = Module.cwrap('kcecodename','string',['number']);
    kcdbecode = Module.cwrap('kcdbecode','number',['number']);
    kcdbclose = Module.cwrap('kcdbclose','number',['number']);
    kcdbdel = Module.cwrap('kcdbdel',null,['number']);

    db = kcdbnew();
    if (!kcdbopen(db, "-", KCOWRITER | KCOCREATE)) {
        console.log("open error: " + kcecodename(kcdbecode(db)));
    }
    if (!kcdbset(db, "foo", 3, "hop", 3) ||
        !kcdbset(db, "bar", 3, "step", 4) ||
        !kcdbset(db, "baz", 3, "jump", 4)) {
        console.log("set error: " + kcecodename(kcdbecode(db)));
    }
    vbuf = kcdbget(db, "foo", 3, 256);
    if (vbuf) {
        console.log(vbuf);
    } else {
        console.log("get error: " + kcecodename(kcdbecode(db)));
    }
    if (!kcdbclose(db)) {
        console.log("close error: " + kcecodename(kcdbecode(db)));
    }
    kcdbdel(db);


Live demo: [demo.html][1]


  [1]: https://rawgithub.com/vulture0/LibKyotoCabinet.js/master/index.html