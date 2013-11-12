IRC protocol support for the XP Framework
========================================================================
 
Usage example:

```php
use peer\irc\IRCConnection;
use util\log\Logger;
use util\log\ConsoleAppender;

$c= new IRCConnection(new IRCUser('MyBot'), 'irc.xxx.net');

// Add logging
$cat= Logger::getInstance()->getCategory();
$cat->addAppender(new ConsoleAppender());
$c->setTrace($cat);

// Add listener
$c->addListener(new MyBotListener());
$c->open();
$c->run();
$c->close();
```

The `MyBotListener` class should subclass the abstract `IRCConnectionListener`
base class, overwriting one or more of the following template methods:

```groovy
public abstract class peer.irc.IRCConnectionListener extends lang.Object {
  public void onPings(peer.irc.IRCConnection $connection, string $data)
  public void onConnect(peer.irc.IRCConnection $connection, string $server, int $port)
  public void onDisconnect(peer.irc.IRCConnection $connection, string $server, int $port)
  public void onMOTDStart(peer.irc.IRCConnection $connection, string $server, string $target, string $data)
  public void onMOTD(peer.irc.IRCConnection $connection, string $server, string $target, string $data)
  public void onEndOfMOTD(peer.irc.IRCConnection $connection, string $server, string $target, string $data)
  public void onServerMessage(peer.irc.IRCConnection $connection, string $server, int $code, string $target, string $data)
  public void onInvite(peer.irc.IRCConnection $connection, string $nick, string $who, string $channel)
  public void onKicks(peer.irc.IRCConnection $connection, string $channel, string $nick, string $who, string $reason)
  public void onQuits(peer.irc.IRCConnection $connection, string $channel, string $nick, string $reason)
  public void onNickChanges(peer.irc.IRCConnection $connection, string $nick, string $new)
  public void onJoins(peer.irc.IRCConnection $connection, string $channel, string $nick)
  public void onParts(peer.irc.IRCConnection $connection, string $channel, string $nick, string $message)
  public void onModeChanges(peer.irc.IRCConnection $connection, string $nick, string $target, string $mode, string $params)
  public void onPrivateMessage(peer.irc.IRCConnection $connection, string $nick, string $target, string $message)
  public void onTopic(peer.irc.IRCConnection $connection, string $nick, string $channel, string $topic)
  public void onNotice(peer.irc.IRCConnection $connection, string $nick, string $target, string $message)
  public void onAction(peer.irc.IRCConnection $connection, string $nick, string $target, string $action)
  public void onVersion(peer.irc.IRCConnection $connection, string $nick, string $target, string $params)
  public void onUserInfo(peer.irc.IRCConnection $connection, string $nick, string $target, string $params)
  public void onClientInfo(peer.irc.IRCConnection $connection, string $nick, string $target, string $params)
  public void onPing(peer.irc.IRCConnection $connection, string $nick, string $target, string $params)
  public void onTime(peer.irc.IRCConnection $connection, string $nick, string $target, string $params)
  public void onFinger(peer.irc.IRCConnection $connection, string $nick, string $target, string $params)
  public string hashCode()
  public bool equals(lang.Generic $cmp)
  public string getClassName()
  public lang.XPClass getClass()
  public string toString()
}
```