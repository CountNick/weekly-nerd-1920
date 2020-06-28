# Inleiding

Tijdens de meesterproef van de minor web development heb ik samen met een klasgenot samen gewerkt. Hij gaf aan nog niet eerder samen te hebben gewerkt aan een project. Zelf heb ik wel een aantal keren samengewerkt met klasgenoten aan dezelfde Github repo. Wat ik normaal gewend ben om te doen met een samenwerking is om van te voren afspraken te maken over code stijl, het maken van branches, mergen, css of sass etc. Deze keer ben ik dat helemaal vergeten ter sprake te brengen, en mijn teamgenoot heeft dit ook niet gedaan.

# Goede afspraken maken

Op een gegeven moment kwamen wij erachter dat er toch wel wat afspraken van te voren gemaakt moesten worden voor bijvoorbeeld het opslitsen van CSS code. Wij hadden namelijk eerst een groot CSS bestand waar alles in stond. Dit was heel erg onhandig, telkerns als er iets veranderd moest worden(wat best vaak was) moest je door het hele CSS bestand zoeken naar de regel die je wilde veranderen.

# Component wise werken

Na de eerste week hadden wij afgesproken om all onderdelen van de wesbite in componeneten te verdelen. Aangezien de css zou groot werd leek het mij ook wel handig hetzelfde te doen met de CSS. Zo zijn wij tot de oplossing gekomen om voor elk component dat wij maakten, een geleiknamig css bestand te maken. In dit CSS bestand stond alleen de styling van het component met dezelfde naam als het CSS bestand. Al deze CSS bestanden werden elke keer als wij op save drukten gecompiled met Gulp om hier 1 groot css bestand van te maken. 

bijvoorbeeld:

* template bestand:
    playlist.ejs
* CSS bestand:
    playlist.css


# Afspraken nakomen

Dit was een fijne werkmethode alle css was op deze manier vrij makkelijk te vinden en het was fijn dat er snel een nieuw CSS bestand aangemaakt kon worden voor een nieuw component. Dit is ook erg goed gegaan tot een bepaald moment. Op een gegeven moment begon de tijd te dringen. Het ontwerpen van de applicatie kwam in een stroomversnelling en dit veroorzaakte nogal wat stress bij ons. Door het stressen hebben wij niet meer voor elk aparte component een CSS bestand gemaakt. Dit resulteerde erin dat er CSS regels zijn toegevoegd bij bepaalde CSS bestanden die hier niet perse bij hoorde. Dit maakte het weer lastig om sommige regels CSS te vinden.

# Conclusie

Op een gegeven moment hadden wij een werkmethode die goed werkte. Op een gegven moment is dit fout gegaan omdat we allebei in de stress schoten en dingen graag snel wilden oplossen. Hierdoor zijn wij uiteindelijk toch weer ongeorganiseerd te werk gegaan waardoor het proces soms ook moeizamer ging.

# Sources

* https://www.freecodecamp.org/news/css-naming-conventions-that-will-save-you-hours-of-debugging-35cea737d849/
* https://medium.com/@drublic/css-naming-conventions-less-rules-more-fun-12af220e949b
* https://css-tricks.com/bem-101/