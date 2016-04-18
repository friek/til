# Random SOAPClient and XML errors

It turns out that, when you're using PHP in a multithreaded environment such as
php+fastcgi or php+modphp, code involving SOAPClient or actually anything involving
libxml may break when some part of the code called libxml_disable_entity_loader(true).

There are a few bug reports on bugs.php.net describing this phenomenon:

1. https://bugs.php.net/bug.php?id=64938
1. https://bugs.php.net/bug.php?id=62577

The actual problem is that the changed state is shared between threads.

The workaround is to always call libxml_disable_entity_loader(false) when external entities
(think: external WSDL files, DTD files or schema files) need to be loaded.
