# I templates di Django

È l'ora di visualizzare alcuni dati! Django ci dà alcuni **template tags** già pronti per farlo.

## Cosa sono i template tags?

In HTML non puoi scrivere codice Python, perché i browser non lo capiscono. Essi conoscono solo l'HTML. Noi sappiamo che l'HTML è piuttosto statico, mentre Python è molto più dinamico.

I **Django template tags** ci permettono di trasferire le cose simili a Python in HTML, in modo che tu possa costruire siti web in modo più veloce e facile. Accidenti!

## Mostra il template con la lista di post

Nel capitolo precedente abbiamo dato al nostro template una lista di posts nella variabile `posts`. Adesso lo mostreremo nell'HTML.

Per stampare una variabile nel template Django, usiamo doppie parentesi graffe con il nome della variabile all'interno, così:

```html
{{ posts }}
```

Prova questo nel tuo template `blog/templates/blog/post_list.html`. Sostituisci tutto dal secondo `<div>` al terzo `</div>` con `{{ posts }}`. Salva il file e aggiorna la pagina per vedere i risultati:

Come vedi, quello che abbiamo è:

    <QuerySet [<Post: My second post>, <Post: My first post>]>
    

Significa che Django lo vede come una lista di oggetti. Ricordi dalla **Introduzione a Python** come possiamo rendere visibili le liste? Sì, con for loops! In un template Django si fanno così:

```html
{% for post in posts %}
    {{ post }}
{% endfor %}
```

Prova ad inserirlo nel tuo template.

Funziona! Ma noi vogliamo che vengano mostrate come i post statici che abbiamo creato prima nel capitolo **Introduzione ad HTML**. Puoi mischiare i tag HTML con quelli di template. Il nostro `body` avrà questo aspetto:

```html
<div>
    <h1><a href="/">Django Blog</a></h1>
</div>

{% for post in posts %}
    <div>
        <p>published: {{ post.published_date }}</p>
        <h1><a href="">{{ post.title }}</a></h1>
        <p>{{ post.text|linebreaksbr }}</p>
    </div>
{% endfor %}
```

{% raw %}Tutto quello che hai messo tra `{% for %}` e `{% endfor %}` Sarà ripetuto per ciascun oggetto della lista. Aggiorna la tua pagina:{% endraw %}


Ti sei accorto che abbiamo utilizzato una notazione leggermente diversa questa volta `{{ post.title }}` oppure `{{ post.text }}`? Stiamo introducendo i dati in ciascuno dei campi definiti nel nostro modello `Post`. Inoltre le `|linebreaksbr` stanno spingendo il testo dei post attraverso un filtro per trasformare le line-breaks in paragrafi.

## Un' ultima cosa

Sarebbe bello vedere se il tuo sito funziona ancora su Internet, giusto? Proviamo a fare il deploy su Heroku di nuovo. Ecco un riepilogo dei passaggi...

*   Prima di tutto, fai il push del tuo codice verso Heroku

    $ git status
    [...]
    $ git add --all .
    $ git status
    [...]
    $ git commit -m "Modified templates to display posts from database."
    [...]
    $ git push heroku master
    

Congratulazioni! Ora vai avanti e prova ad aggiungere un nuovo post nel tuo Admin Django (ricorda di aggiungere una published_date!), sucessivamente aggiorna il tuo sito per vedere se il post compare.

Funziona come un incantesimo? Ne sono fiero! Staccati dal computer per un po', ti sei guadagnato/a una pausa. :)

![Figura 13.4][6]

 [6]: images/donut.png
