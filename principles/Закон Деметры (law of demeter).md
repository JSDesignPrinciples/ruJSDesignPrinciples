# Low of demeter
## Примерная схема

### Краткое описание
Что это, зачем нужно и как помогает
Пример с точками
Пример с кошельком и деньгами

### История
Почему так называется, кто придумал
### Примеры
#### Чистый JavaScript
Как это работает в JS

#### Чейнинг в underscore | jquery
Нарушает ли принцип деметры?

#### Разрешение зависимостей и инжектор в ангулар
Нарушает ли принцип деметры?

#### Тестирование
Что нужно знать о ПД при тестировании 

## Заключение 
Написать, что это хорошо, но увлекаться не стоит, и всегда нужно искать баланс.


 




## Links
### General links
Wiki
http://en.wikipedia.org/wiki/Law_of_Demeter

http://c2.com/cgi/wiki?LawOfDemeter

Really nice collection of links
http://www.ccs.neu.edu/home/lieber/LoD.html

How does the Law of Demeter apply to object-oriented systems regarding coupling and cohesion? [closed]
http://programmers.stackexchange.com/questions/214721/rails-law-of-demeter-confusion

some of the pretty old stuff
http://don.fed.wiki.org/view/law-of-demeter/sfw.c2.com/law-of-demeter-revisited

Do fluent interfaces violate the Law of Demeter - applies to Javascript as well
http://stackoverflow.com/questions/67561/do-fluent-interfaces-violate-the-law-of-demeter

### JavaScript links

Promises and law of demeter:
http://stackoverflow.com/questions/20275957/does-deferred-promise-promote-breaking-the-law-of-demeter

 Derick Bailey on LoD, see comments
http://lostechies.com/derickbailey/2010/03/25/law-of-demeter-extension-methods-don-t-count/

Backbone and LoD
http://zen-hacking.com/backbone-views-and-the-law-of-demeter/

Nice generalization + some discussion
https://plus.google.com/+TadDonaghe/posts/jRvNenACand

Angular docs: Passing the injector breaks the Law of Demeter. 
https://docs.angularjs.org/guide/di

Part of a Book: Dependency Injection with AngularJS (Holy shit, did not know this kind of book even exists)
http://books.google.com/books?id=9dtdAgAAQBAJ&pg=PT61&lpg=PT61&dq=law+of+demeter+angular&source=bl&ots=AjDR10eAtM&sig=Lo3UjKIxgLtujsEl8L2doLChJwU&hl=en&sa=X&ei=FN-9U4KZE4yryASt8oLgCw&ved=0CC4Q6AEwAg#v=onepage&q=law%20of%20demeter%20angular&f=false

Transfer injector broke The law of Demeter(Law of Demeter, Least knowledge principle)
http://www.programering.com/a/MTO1EzMwATg.html


### Other languages

original article about law of demeter
http://www.ccs.neu.edu/research/demeter/papers/law-of-demeter/oopsla88-law-of-demeter.pdf

Weird stuff
http://www.daedtech.com/visualization-mnemonics-for-software-principles

Ruby examples + some discussion 
http://devblog.avdi.org/2011/07/05/demeter-its-not-just-a-good-idea-its-the-law/
http://guillecarlos.com/refactoring-law-of-demeter.html
https://practicingruby.com/articles/temporal-coupling-and-the-law-of-demeter
http://programmers.stackexchange.com/questions/214721/rails-law-of-demeter-confusion
http://rails-bestpractices.com/posts/15-the-law-of-demeter
http://www.informit.com/articles/article.aspx?p=1834700&seqNum=6

"I've always felt I'd be more comfortable with the Law of Demeter if it were called the Suggestion of Demeter." Martin Fowler
http://martinfowler.com/articles/mocksArentStubs.html

Some erlang stuff
http://erlang.org/pipermail/erlang-questions/2013-January/071991.html


Some PHP examples
http://www.sitepoint.com/introduction-to-the-law-of-demeter/

Money And Wallet methaphor
http://juristr.com/blog/2009/09/law-of-demeter-nice-metaphor/

Some .NET stuff
http://lostechies.com/derekgreer/2008/06/10/distilling-law-of-demeter/
http://haacked.com/archive/2009/07/14/law-of-demeter-dot-counting.aspx/
http://taswar.zeytinsoft.com/2009/04/03/law-of-demeter-principle-of-least-knowledge/
http://fusion.dominicwatson.co.uk/2012/07/the-law-of-demeter.html

Misunderstanding the Law of Demeter
http://www.dan-manges.com/blog/37

Law of Demeter is easy to spot when you need extra mocks
http://richarddingwall.name/2009/08/26/law-of-demeter-is-easy-to-spot-when-you-need-extra-mocks/

Refactoring to Law of Demeter
http://pilchardfriendly.wordpress.com/2009/04/06/refactoring-to-law-of-demeter/?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%3A+PlanetTw+%28Planet+TW%29

OO: Reducing the cost of…lots of stuff!
http://www.markhneedham.com/blog/2009/03/12/oo-reducing-the-cost-oflots-of-stuff/

>> done.for.the.day.about.to.go.to.the.hotel.where.i.specificatlly.wont.think.about.the.law.of.demeter() 

Some java stuff
http://misko.hevery.com/2008/07/18/breaking-the-law-of-demeter-is-like-looking-for-a-needle-in-the-haystack/
http://java.dzone.com/articles/law-demeter
http://vitalflux.com/law-demeter-violations-fix/
http://www.ericfeminella.com/blog/2008/02/02/principle-of-least-knowledge/

### Not just demeter
http://www.bennadel.com/blog/2375-object-calisthenics-in-javascript-my-first-attempt.htm

http://habrahabr.ru/post/206802/
### Russian

Nice discussion
http://toster.ru/q/44822

Несвязность_и_закон_Деметра
http://ru.wikibooks.org/wiki/%D0%9D%D0%B5%D1%81%D0%B2%D1%8F%D0%B7%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D0%B8_%D0%B7%D0%B0%D0%BA%D0%BE%D0%BD_%D0%94%D0%B5%D0%BC%D0%B5%D1%82%D1%80%D0%B0

http://plakhov.livejournal.com/54739.html

Ruby looks like a translation
http://vessi.github.io/blog/2012/07/18/zakon-diemietry-ili-poakkuratnieie-s-tochkami/

http://life-prog.ru/view_zam2.php?id=174&cat=5&page=8
