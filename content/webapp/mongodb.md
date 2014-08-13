MongoDB
=======

    var mongoose = require('mongoose');
    var passport = require('passport');
    var Account = require('./models/account');

    // ...
    // app.use(express.session());
    app.use(passport.initialize());
    app.use(passport.session());
    // app.use(app.router);
    // ...

    passport.use(Account.createStrategy());
    passport.serializeUser(Account.serializeUser());
    passport.deserializeUser(Account.deserializeUser());

    mongoose.connect('mongodb://127.0.0.1/resume');

    app.get('/register', function(req, res) {
        res.render('register', { });
    });

    app.post('/register', function(req, res) {
        Account.register(new Account({ username : req.body.username }), req.body.password, function(err, account) {
            if (err) {
                return res.render('register', { account : account });
            }

            res.redirect('/');
        });
    });

    app.get('/login', function(req, res) {
        res.render('login', { user : req.user });
    });

    app.post('/login', passport.authenticate('local'), function(req, res) {
        res.redirect('/');
    });

    app.get('/logout', function(req, res) {
        req.logout();
        res.redirect('/');
    });