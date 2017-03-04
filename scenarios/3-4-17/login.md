# Login

## Description

An anonymous user arrives at the site and sees a splash page with "Sign in with Google"

A user clicks "Sign in with Google" and sees a Google window open in the page

The user authorizes the site to access their email

The user sees the Google window close and the page change to their dashboard page

The user selects "sign out" and sees the page change to the splash page with "Sign in with Google"

### Responses

#### Cameron

1. In re: invitation/requirement to login occurring at every request state, I was describing specifically the splash page.  I don't think this scenario describes other paths/states, merely the state of: splash page (www.example.com) + anonymous user.

2. In re: mapping of request paths and actions.  I think _No_.  I think that's an important element of what makes this not just Swagger API + semantic sugar.  I believe some "pages/actions/views/states" are comprised of _multiple_ requests/paths, and some might be none (?) - the point is it's just describing the actual displayed behavior, with enough detail to extrapolate front-end and back-end specifics.

3. In re: splash screen descriptiveness - I like it.  So then we have two conditionals + location to describe the "action" (we need to nail down the taxonomy here) - "splash page + anonymous user + redirect info" - I like this, because it also means the page after "sign out" would be loaded.  Obvious implementation is get param but that's getting to implementation not interface, right?

4. In re: google users -> users, I think for pages that use Google OpenID connect, yes (the specific scenario here).  In the same way as another app would use InterSIS OpenID Connect and would need InterSIS user-> our user mapping.

5. In re: classes of users, for this scenario I was only getting as far as "show their dashboard" not speccing the dashboard.  I think that decision wouldn't need to be made until speccing the dashboard, right?

6. Counter-question: is it possible to be a user at www.learnthestates.com and a user at ysd.ak.learnthestates.com?
  - Pro: you can still make an account after you leave school X without getting a new google account.
  - Con: (like with typingclub) can result in classroom confusion
  

#### Joseph

1. Does the invitation/requirement to login occur at every request path/state, or just some request paths/states?

  If just some, then need a system to that maps request paths/states to login required/optional/irrelevant.
  
2. Speaking of which, is there a one to one mapping between request paths and actions?

  Or is the idea of a request path too web specific? Like is a request path not a concept that applies to our mobile applications?
  
  Or maybe there's something similar to a request path, like a hierarchy of actions. EG: the password change action lives inside of the profile action lives inside of the user controls action, and on a web client that's "mapped" by /user-controls/profile/change-password, and for our mobile clients there's a directly analogous mapping.

3. Perhaps on the "splash screen" there's some information, that varies with what page the user wants to see?

  Like, the user googled "How to Do Z on Sigma Education" and they follow a good link to Do "Z" on our site. And the landing page says, "All your friends will love you after you've done Z, and you're just one step away! Login with Google to start doing Z today." And then there's the blue Google button.
  
  But if the user had arrived at the "Do X" page, then the info would be different.
  
  So maybe this suggests that the spec should have different branches or something for people in different login states.
  
4. Looks like we'll need a table in our database that associates Google users with our users!

5. Are there different classes of users?

  Like students vs teachers, and if you land on the "Do Z" page as a student it says, "Doing Z is only for teachers. You can try signing out, and signing back in with your teacher account.
  
  And maybe there are "free" students and "premium" students and "free" teachers and "premium" teachers? And they should get different "pages" for the same requests.
  
6. Maybe we've got different sites, like www.learnthestates.com for just anyone who comes off of the web to learn about the states, but also ysd.ak.learnthestates.com for those from YSD who want to learn the states.

  And if so, then what if I drop into www.learnthestates.com and I sign in with Google, but I'm also a client of ysd.ak.learnthestates.com? Should I be informed that, hey, you've also got an account at ysd.ak.learnthestates.com and maybe you'd like to use that instead?

### Response to Responses

#### Cameron

#### Joseph
