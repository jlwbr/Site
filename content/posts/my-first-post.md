---
title: De reis in het bouwen van mijn site
date: 2018-06-04T19:29:58.000Z
draft: false
gitment: true
slug: gitment-journey
---
Ik heb dit domein al een tijdje, heb er eigenlijk maar weinig me gedaan, vooral tests waar ik een domein voor nodig had. Al speelt het idee om hier een blog van te maken al sinds de aankoop. Dus dacht ik aan het begin van deze week, laat ik dat eens doen.

De reis die me tot deze site heeft geleid is het verhaal voor deze post.

Ik speel al een tijdje met Static Site Generators en tot nu toe bevallen ze me goed, dus dat is wat ik voor mijn blog heb gebruikt. Tot nu toe had ik alleen nog maar ervaring met [Jekyll](https://jekyllrb.com/) dit omdat het de Generator voor Github Pages is. Nou werkt Jekyll erg goed en ben ik tevreden met de functies, maar voor mijn blog wou ik toch eens wat anders proberen, dus na een snelle check op [staticgen.com](https://www.staticgen.com/) vond ik de op 1 na populairste Static Site Generator, Hugo. De features stonden mij wel aan, een super snelle build tijd(minder dan 1ms per pagina), markdown support en i18n support zonder plugins.

Het opzetten van mijn site ging aardig makkelijk, installeer de cli, run hugo new site en je site draait, ik ben lui als het op de frontend aankomt en heb een van de vele [themes](https://themes.gohugo.io/) gekozen, want standaard waarden aanpassen, en vouila een prachtige snel ladende site, een probleem de comments, omdat ik een static site generator gebruik kan kan moeilijk dinamische content laden, Disqus, de populairste oplossing stond me niet aan vanwege privacy en de traagheid van hun systeem, facebook comments zelfde verhaal, na lang zoeken kwam ik uit op [Gitment](https://github.com/imsun/gitment/).

Gitment zag er gelikt uit, het gebruikt Github issues voor de comments en laat deze dan onder de bogpost manier aan je zien. Opzetten was ook super makkelijk, voeg de css + javascript toe aan elke pagina waar je comments wil hebben, maak een nieuw Gitment object en voeg er wat config variablen aan toe, klaar is kees. Voor Hugo is dit nog wel een dingetje, omdat dit natuuklijk automatisch moet gebeuren bij elke post, maar ook dit bleek niet zo'n groot probleem. Voeg de css + js toe aan de post partial van je theme en ook dit probleem is obgelost, om er voor te zorgen dat elke post zijn eigen issue krijgt kun je een slug toevoegen aan de font matter van je post, de code die ik hiervoor heb gebruikt is:

{{< highlight javascript "linenos=table" >}}

{{ if (.Params.gitment) }}

  <div id="git-comments"></div>
  <link rel="stylesheet" href="https://imsun.github.io/gitment/style/default.css">
  <script src="https://imsun.github.io/gitment/dist/gitment.browser.js"></script>
  <script>
    const gitment = new Gitment({
      id: '{{ .Slug }}',
      owner: 'jlwbr',
      repo: 'site',
      oauth: {
        client_id: 'jouw client id',
        client_secret: 'jouw client secret',
      },
    })
    gitment.render('git-comments')
  </script>
{{ end }}

{{< / highlight >}}

Deze code zorgt ervoor dat gitment alleen wordt toegevoegd bij paginas die ook echt comments hebben, dit wordt gedaan door de if statement die ervoor zorgt dat  alleen aan posts met de font matter gitment: true deze code wordt toegevoegd. Comments check.

Nu de hosting nog, dit was voor mij een no brainer, Netlify. Het lijkt alsof ik hier een beetje reclame zit maken voor ze, maar het is echt een geweldige service. Ze kunnen overweg met letterlijk elke static site generator en hebben verschillende services om je leven makkelijker te maken. Met een simpele [netlify.toml](https://github.com/jlwbr/Site/blob/master/netlify.toml) in de root dir weet netlify genoeg en bouwen ze je site voor je zonder enige moeite. Ook hebben ze gratis Letsencrypt Certs dus ssl is ook zo geregeld. Ik raad ze zeker aan.

Zo dat was hem dan. Mijn eerste blog post. Ik hoop dat je er wat aan heb gehad, en mogen er vele volgen.
