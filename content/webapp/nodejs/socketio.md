Socket.io
=========

Duplicated Response
-------------------

A common mistake when start using Socket.io is to put ``socket.emit()`` right next to ``socket.on()``, which seems natual.

    #!javascript
    function foo() {
        socket.emit('req');
        socket.on('res', function(data) {
            console.log(data);
        })
    }

However this will result in duplicated actions, since every time ``foo()`` is called, one ``res`` is registered. To fix this, move ``socket.on()`` out of the function, make sue it is only called once.

    #!javascript
    function foo() {
        socket.emit('req');
    }


    socket.on('res', function(data) {
        console.log(data);
    }) 
 

