# pasport_auth

## Install
```npm
$ npm install passport-local
```
Usage
Configure Strategy
The local authentication strategy authenticates users using a username and password. The strategy requires a verify callback, which accepts these credentials and calls done providing a user.
```js
passport.use(new LocalStrategy(
  function(username, password, done) {
    User.findOne({ username: username }, function (err, user) {
      if (err) { return done(err); }
      if (!user) { return done(null, false); }
      if (!user.verifyPassword(password)) { return done(null, false); }
      return done(null, user);
    });
  }
));
```
## Authenticate Requests
Use passport.authenticate(), specifying the 'local' strategy, to authenticate requests.

For example, as route middleware in an Express application:

```js
app.post('/login', 
  passport.authenticate('local', { failureRedirect: '/login' }),
  function(req, res) {
    res.redirect('/');
});
```
