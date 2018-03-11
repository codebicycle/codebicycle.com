# Session Fixation

Session fixation and session hijacking are both attempts to gain access to a system as another user.

> causes a victim to use a session id chosen by an attacker

## Protection

Delete the old session id and create a new session id, when authenticating a user.

- A sells a car to B
- A doesn't give all of the keys to B and keeps one
- If B doesn't change the lock, A could still use it.


If the session id remains the same before and after log-in, it is vulnerable.

- specific to session implementations that use a session Id.  
  Flask by default doesn't use a session Id.

## Process

Attacker A gives a session id to B
After B authenticates, the server does not update the session id value
A can use the session id to log in to B's account.

## Example

Amazon

When someone goes to Amazon they can add products in cart without logging in.  
When they decide to log in, Amazon links the unauthenticated session data with the authenticated user

If Amazon did not create a new session id on authentication:

- an attacker might go to Amazon first
- get an unauthenticated session id
- fixate that session id in the victim browser and wait for it to log in
- after the victim logs in, with the attacker fixated session, the attacker refreshes their browser and they will be authenticated as the victim.


## Sources
Hanqing Wu, Liz Zhao. (2015). Web Security, Auerbach Publications  
[Session Fixation Demystified][session-fixation-demystified] (2014) 

[session-fixation-demystified]: http://www.lanmaster53.com/2014/10/29/session-fixation-demystified/
