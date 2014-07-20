# Law of demeter
a specific case of loose coupling.
## Примерная схема
### Краткое описание и как понять что закон нарушен

Что это, зачем нужно и как помогает

Слишком большое количество точек (может нет, а может да)

`a.b().c().d()` так же плохо как и `b = a.b(); c = b.c(); c.d()` 

Закон деметры был сформулирован не для JavaScript и слепо применять его нельзя Однако польза от него может быть

Мы постараемся разобраться объективно, где в JS стоит, а где не стоит применять закон деметры.


### История

Был придуман в 1987 году во время разработки проекта деметра.

Изначально был сформулирован для 4х языков: Smalltalk, CLOS, C++ и Eiffel

Альтернативным названием  предложенным в статье было скромное "Правило хорошего стиля" (now known in-house as the Law of Demeter or the Law of Good Style)

Проект по ходу сдох(пруф? ), а закон остался http://www.ccs.neu.edu/home/lieber/what-is-demeter.html

Проект был назван в честь богини деметры, потому что в чуваков которые разрабатывали его был набор железа Зевс, с которым система должна была работать. Деметра - сестра зевса


#### Пара абстрактных примеров, чтобы было понятно о чем речь

Тут пример с заказами в последнем посте http://c2.com/cgi/wiki?LawOfDemeterMakesUnitTestsEasier

Пример, где отдаешь кошелек вместо того, чтобы отдать деньги [1]

Пример где не говоришь собакиной ноге что делать

Для неймспейса наверное не должно применяться. Например если есть сложный json, то client.info.address.line2 по идее ничего не нарушает

http://en.wikipedia.org/wiki/Multilayered_architecture
## Зачем нам это нужно и к чему это может привести 
### Плюсы

* Видны и понятны все зависимости функции и класса
* проще тестировать, потом что не надо создавать вложенные моки
* Меньше всего менять (объснить)
* Посволяет избавиться от ошибок, когда внешний класс не в курсе, что внутренний класс был изменен
* Возможно меньше печатать
http://alvinalexander.com/java/java-law-of-demeter-java-examples

### Минусы  

* Больше функций в интерфейсе 
* Нарушает Narrow interfaces
* Найти может быть довольно просто, но вот починить - не всегда, иногда пытаясь починить можно сделать еще хуже
todo: The LawOfDemeter minimizes logical coupling, but maximizes what could be called "physical coupling" -- the number of instantiated objects that need to be traversed for any particular operation. There are specific reasons why this might be bad. If performance is an issue, you might not want to incur the costs of implicitly navigating through a bunch of objects every time you call a top-level method. (This can be counteracted by caching intermediate objects, though that might be cumbersome in practice.) Similar issues can occur when you're using multithreading or distributed systems, where physical indirection can cause problems.

## Примеры
Дальше мы пройдемся по примерам и для каждого посмотрим, даст ли применение ЗД обещанные выше плюсы, и удастсяли избежать минусов

#### Чистый JavaScript
Как это работает в JS

#### Чейнинг в underscore | jquery
Нарушает ли принцип деметры?
utils.measurments.size( something )

#### Разрешение зависимостей и инжектор в ангулар
Нарушает ли принцип деметры?


### Тестирование

* Что нужно знать о ПД при тестировании 
* Не нужно создавать моки вложенный в моки и не нужно знать как фигня работает внутри.


### Заключение 
Везде нужен баланс
Как сказал мартин фоулер, "I've always felt I'd be more comfortable with the Law of Demeter if it were called the Suggestion of Demeter."


-------
# Example with Order.Client.name
Возможное решение: 
order.clientName
Минусы: нужно делегировать каждое свойство
Плюсы : Если какой-то свойство перенесется, шаблоны менять не нужно
# Example with a paper boy and a wallet
## Original
```Javacript
function Wallet( money ){
    this.money = money;
}

Wallet.prototype.getMoney = function( amount ){
    // get the money
}

function Customer( wallet, name ){ 
    this.wallet = wallet
    this.name = name;
}
Customer.prototype.getWallet = function(){
  return this.wallet;
}

function PaperBoy(){
   
}

PaperBoy.prototype.acceptPayment = function( customer ){
    var wallet = customer.getWallet(); 
    if( wallet.hasMoney( amount ) ){
        wallet.getMoney( amount );
    }
    // LOD broken
}
```
Что здесь не так, и почему это нужно исправлять?
1. Если нужно будет добавить кредитную карточку, то будет геморрой
2. Если появится кто-то еще, кто хочет получить деньги с клиента, придется дублировать код с проверками
3. Клиент позволяет любому классу управлять свои коешльком, что не всегда желательно
4. TODO
## Solution 1

```Javacript
Customer.prototype.getMoney = function( amount ){
  return this.wallet.getMoney( amount )
}
```
Плюсы: 
* PaperBoy is decoupled from the wallet class 
* PaperBoy con not do bad things with the wallet
Минусы: 
* Если делать так часто, слишком много методов будет у кастомера.

## Solution 2  

```Javacript
PaperBoy.prototype.acceptPayment = function( wallet ){
    wallet.getMoney(); 
}
```
Плюсы: 
* PaperBoy ничего не знает про кастомера
// TODO подрбнее  и больше примеров 
## Solution 3  

```Javacript
var paymentService = {
    processPayment: function( fromWallet, toWallet, amount){
        // do the payment
    }
}

PaperBoy.prototype.acceptPayment = function( customer ){
    paymentService.processService( customer.wallet ); 
}
```
Плюсы: 

// TODO подрбнее  и больше примеров 

# Ссылки и прочие материалы для подготовки статьи
 
 
## Вопросы и вещи которые пока непонятны
* Как это работает с функциональным программированием?
* А как с фабриками? SomeFactory.createSomething().doSomething()
* Как это связано с TellDontAsk ?
* Как это все соотносится с замыканиями?
* Как это все соотносится с промисами? Есть вопрос на СО, но там никто не понимает, что происходит http://stackoverflow.com/questions/20275957/does-deferred-promise-promote-breaking-the-law-of-demeter
* jQuery
* chaining in underscore?
* Функции которые приходят в качестве аргументов?
* Библиотеки. Вся эта фигня, чтобы если интерфейс объекта поменяется, не было боли. Библиотеки меняются редко, поэтому там можно простить нестинг и чейнинг?
* Moжно ли отследить нарушения принципа с помощью статического анализа?
* Определен ли закон на уровне функии или на уровне класса?
* Массивы объектов - исключение из правила
* How is this at all related to bridge and shield patterns?
* Domain specific objects only?
* Coffee script has a ? operator, talk about it and LoD # http://haacked.com/archive/2009/07/14/law-of-demeter-dot-counting.aspx/ 

## Цитаты
, it's a guidline to help reduce coupling in code

Taken from http://www.ccs.neu.edu/home/lieber/LoD.html: 2003 was the 15 Year Anniversary of the Law of Demeter: The Law of Demeter is a simple style rule for designing ObjectOriented systems. "Only talk to your immediate friends" is the motto. The style rule was first proposed at Northeastern University in the fall of 1987 and popularized in books by Booch, Budd, Coleman, Larman, Page-Jones, Rumbaugh and others. A 2000 book that describes it well is The Pragmatic Programmer by AndrewHunt and DavidThomas. The name "Law of Demeter" was chosen because the style rule was discovered while working on the The Demeter Project which ever since was strongly influenced by the Law of Demeter. The Demeter Project develops tools that make it easier to follow the Law of Demeter. (Demeter = Greek Goddess of Agriculture; grow software in small steps) For example, "only talk to your immediate friends that share the same concerns" leads to tools for Aspect-Oriented Software Development.

Demeter has raised (ага)what we would know here as a CodeSmell to the level of a law. 

 Demeter tries to establish a relation about objects created and used within a method or function,
 
 Something about telling the milk to uncow itself...?
 
 
 The Demeter system considers Repetition objects as special classes of objects for which the oft-quoted normal Demeter "law" does not apply in the same manner. In fact, the Demeter method/system contains several laws/forms of Demeter, each of which applies to its appropriate context (which is still admittedly broad and abstract) and is not completely universal in applicability. People just tend to hear only about the form that is most commonly cited and not always with the appropriate context. Even so, for regular OOD/OOP, it's still more of a guideline (a very strong recommendation) rather than a hard and fast, inviolable rule.


The Demeter literature talks about the introduction of <b>lots</b> of additional small methods, which started getting unwieldy to add manually, and is part of why the Demeter tools exists, so they can be autogenerated as needed.
This gets into issues of propagation of results of partial computations, which is a whole other area of Demeter called "propagation patterns" (not be confused with "design patterns"). Beyond the straightforward stuff, trying to go "full" Demeter without the niceties of the "full" Demeter system has lots of not niceties" associated with it because without Demeter's tool-support you can't so easily propagate what is needed where in an orthogonal fashion. -- [[Anonymous Donor]]

 had the opportunity to briefly chat with Michael Feathers about LoD and he pointed out the example of Excel’s object model for tables and cells. If LoD is about encapsulation (aka information hiding) then why would you hide the structure of an object where the structure is exactly what people are interested in and unlikely to change?
 
 Software design principles can be interesting to study in the abstract, but there is no substitute for trying them out in concrete applications. If you can find a project that is a natural fit for the technique you are trying to investigate, even the most simple toy application will teach you more than pure thought experiments ever could.
 
 I think applying the Law of Demeter to individual classes is taking it a bit too far. I think a better application is to apply it to layers in your code. For example, your business logic layer shouldn't need to access anything about the HTTP context, and your data access layer shouldn't need to access anything in the presentation layer.
 
 The style rule was first proposed at Northeastern University in the fall of 1987 by Ian Holland and popularized in books by Booch, Budd, Coleman, Larman, Page-Jones, Rumbaugh and others. A
## Мысли
### Статический анализ
 В языке со статической типизацией можно выяснить, какие классы знают о других классах
 Можно выяснить, какие классы напрямую зависят от других классов
 Если из первого вычесть второе, то будет понятно
 У руби есть какой-то инструмент для находжения нарушений ЗД, надо посмореть внимательнее
  http://www.ccs.neu.edu/research/demeter/DemeterF/
 

### Вариации 
## LoDC
in 2003/2004 the Law of Demeter was revisited for Karl Lieberherr's ICSE 2004 keynote paper and presentation. The Law of Demeter was refined from "Only talk to your friends" to "Only talk to your friends who share your concerns" and this refined form is called the Law of Demeter for Concerns (LoDC). The LoDC is best followed by using Aspect-Oriented Software Development (AOSD) techniques such as AspectJ or DJ. On the other hand, the LoDC leads to better AOSD. Properly following the LoDC has two key benefits: It leads to better information hiding (using the technique of structure-shyness or the more general technique of concern-shyness) and to less information overload for the software developer.



## Links
### General links
Wiki http://en.wikipedia.org/wiki/Law_of_Demeter


http://c2.com/cgi/wiki?LawOfDemeter
http://c2.com/cgi/wiki?LawOfDemeterIsInvalid
http://c2.com/cgi/wiki?LawOfDemeterRevisited
http://c2.com/cgi/wiki?IsLawOfDemeterOverspecifiedOnCeeTwo

Хорошая статья, все отлично расписано, возможно - первоисточник примера с кошельком
http://www.ccs.neu.edu/research/demeter/demeter-method/LawOfDemeter/paper-boy/demeter.pdf
 http://c2.com/cgi/wiki?LawOfDemeterMakesUnitTestsEasier
http://c2.com/cgi/wiki?LawOfDemeterIsHardToUnderstand 
http://c2.com/cgi/wiki?LawOfDemeterIsTooRestrictive // see "How to apply the LawOfDemeter successfully"
http://c2.com/cgi/wiki?LawOfDemeterAndCoupling
http://c2.com/cgi/wiki?CanLawOfDemeterBeRefactoredAutomatically // bullshit
http://c2.com/cgi/wiki?TellDontAsk 

Really nice presenation, great research, Java examples, have to read
http://www.slideshare.net/vladimirtsukur/law-of-demeter-objective-sense-of-style

 ---- Finished here
Really nice collection of links 
http://www.ccs.neu.edu/home/lieber/LoD.html // TODO: Read more carefully, good material in the presentation

How does the Law of Demeter apply to object-oriented systems regarding coupling and cohesion? [closed]
http://programmers.stackexchange.com/questions/214721/rails-law-of-demeter-confusion
http://stackoverflow.com/questions/6918666/law-of-demeter-and-oop-confusion # Good point, answers are not helpful

some of the pretty old stuff
http://don.fed.wiki.org/view/law-of-demeter/sfw.c2.com/law-of-demeter-revisited

Do fluent interfaces violate the Law of Demeter - applies to Javascript as well
http://stackoverflow.com/questions/67561/do-fluent-interfaces-violate-the-law-of-demeter

http://wiki.tcl.tk/8505

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
http://www.daedtech.com/visualization-mnemonics-for-software-principles # Some ridiculous example on handling pants instead of wallet 

 


Ruby examples + some discussion 
http://devblog.avdi.org/2011/07/05/demeter-its-not-just-a-good-idea-its-the-law/
http://guillecarlos.com/refactoring-law-of-demeter.html # Some ruby refactoring from really ugly code to just ugly code
https://practicingruby.com/articles/temporal-coupling-and-the-law-of-demeter # A very hardcore version of demeter law applied to some async thing in ruby. worth revisiting
https://sites.google.com/site/unclebobconsultingllc/active-record-vs-objects # Link from the previous post
http://programmers.stackexchange.com/questions/214721/rails-law-of-demeter-confusion
http://rails-bestpractices.com/posts/15-the-law-of-demeter
http://www.informit.com/articles/article.aspx?p=1834700&seqNum=6
https://github.com/emerleite/demeter
http://www.dan-manges.com/blog/37 # Good example on not just having properties out, but having the logic out, makes more sense

"I've always felt I'd be more comfortable with the Law of Demeter if it were called the Suggestion of Demeter." Martin Fowler
http://martinfowler.com/articles/mocksArentStubs.html

Some erlang stuff
http://erlang.org/pipermail/erlang-questions/2013-January/071991.html


Some PHP examples
http://www.sitepoint.com/introduction-to-the-law-of-demeter/
http://www.theodo.fr/blog/2013/02/dont-overuse-dependency-injection/

Python 
https://mail.python.org/pipermail/python-list/2002-December/152685.html

Money And Wallet methaphor
http://juristr.com/blog/2009/09/law-of-demeter-nice-metaphor/

Some .NET stuff
http://lostechies.com/derekgreer/2008/06/10/distilling-law-of-demeter/
http://haacked.com/archive/2009/07/14/law-of-demeter-dot-counting.aspx/
http://taswar.zeytinsoft.com/2009/04/03/law-of-demeter-principle-of-least-knowledge/
http://fusion.dominicwatson.co.uk/2012/07/the-law-of-demeter.html


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
http://www.blackwasp.co.uk/LawOfDemeter.aspx
http://eyalgo.com/2014/02/17/law-of-demeter-4/
http://theshyam.com/tag/law-of-demeter/
http://www.javacodegeeks.com/2012/06/demeter-law.html

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

http://c2.com/cgi/wiki?InformationHiding
http://vessi.github.com/blog/2012/07/18/zakon-diemietry-ili-poakkuratnieie-s-tochkami/
http://msdn.microsoft.com/ru-ru/magazine/cc947917.aspx

## Books
pragmatic programmer 
Clean code

## testing
http://googletesting.blogspot.com/2008/07/breaking-law-of-demeter-is-like-looking.html
http://programmers.stackexchange.com/questions/232442/unit-testing-factories-and-the-law-of-demeter
http://jayflowers.com/WordPress/?p=78
http://codevanced.net/post/The-Law-of-Demeter-The-crux-of.aspx
http://www.scottmcmaster365.com/2011/04/law-of-demeter-makes-you-create-mock.html

http://stackoverflow.com/questions/19549535/intellij-ideas-law-of-demeter-inspection-false-positive-or-not
https://code.google.com/p/testability-explorer/wiki/LawOfDemeterCostExplanation
http://blog.bbv.ch/2011/03/28/law-of-demeter-and-testability/
http://blog.igorstoyanov.com/2005/10/stubs-or-mocks-state-or-behavior_30.html
https://groups.yahoo.com/neo/groups/extremeprogramming/conversations/topics/122627

## LoD for namespaces and data objects
http://stackoverflow.com/questions/12284057/law-of-demeter-data-objects
http://codereview.stackexchange.com/questions/131/law-of-demeter-and-data-models

## Articles
An Empirical Validation of the Beneﬁts of
Adhering to the Law of Demeter
http://www.ccs.neu.edu/home/lieber/LoD/LoD-2011-Zurich.pdf

#In 2003/2004 the Law of Demeter was revisited for Karl Lieberherr's ICSE 2004 keynote paper and presentation. The Law of Demeter was refined from "Only talk to your friends" to "Only talk to your friends who share your concerns" and this refined form is called the Law of Demeter for Concerns (LoDC). 
http://www.ccs.neu.edu/research/demeter/biblio/icse-2004-keynote.html
http://www.ccs.neu.edu/research/demeter/papers/icse-04-keynote/ICSE2004.pdf

# Coupling and cohesion
http://msdn.microsoft.com/en-us/magazine/cc947917.aspx
http://stackoverflow.com/questions/163071/coupling-cohesion-and-the-law-of-demeter

# TO SORT
http://theknowledge.me.uk/mywiki/concepts/law-of-demeter.html
http://blog.shutupandcode.net/?p=718
