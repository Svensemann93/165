# Cheat Sheet Redis / Modul 165

## Für was wird Redis eingesetzt?

- Redis wird für caching eingesetzt.
- Redis ist eine Datenbankart, eine SQL Datenbank
- Alle Daten sind in "Key Value Pairs" gespeichert
- Es gibt keine Tabellen
- Format JSON
- Redis speichert die Daten nicht auf einer Festplatte 
sondern direkt im RAM
- Redis ist dadurch extrem schnell, bei einem Defekt / Absturz sind alle Daten verloren
- Redis wird dadurch mehr für Caching benutzt, als zum Speichern von Daten. Für solche Dinge wird eher MongoDB oder so benutzt
- Redis wird zu anderen Datenbanken dazugeschaltet, arbeitet also nicht alleinstehend

## Redis-Container starten (mit Docker)

```bash
docker run -d --name my-redis -p 6379:6379 redis
```
## Zugriff auf redis-cli im Container 

```bash
docker exec -it my-redis redis-cli
```
## Zugriff auf redis-cli im Container 

```bash
SET test "Hallo Redis" 
GET test 
FLUSHALL
```
## Aufräumen

```bash
docker stop my-redis     # Stoppt den laufenden Container 
docker rm my-redis       # Entfernt den Container 
docker rmi redis         # (Optional) Entfernt das Redis-Image
```
## Video

- https://www.youtube.com/watch?v=jgpVdJB2sKQ&t=800s

## Redis installieren

```bash
sudo apt-get install redis
```

## Redisserver starten

```bash
redis-server
```

## Redis öffnen

```bash
redis-cli
```

## Redis verlassen

```bash
quit
```

## Daten einfügen

```bash
SET name sven
```

## Daten holen

```bash
GET name 
```
## Daten löschen

```bash
DEL age
```
## Prüfen ob Daten vorhanden

```bash
EXISTS name
```

## Keys nach Value suchen (retourniert alle Keys)

```bash
KEYS *
```

## Alle Werte löschen

```bash
flushall
```
## Time to Live anzeigen

```bash
ttl name
```

## Time to live setzen

```bash
expire name 10
```

```bash
setex name 10  sven
```
- heisst hier, dass sven in 10 Sekunden abläuft

## Listen in Redis

```bash
lpush friends john
```

- so wird der Value john in eine neue Liste gespeichert (am Anfang) mit rpush am Ende.

```bash
lrange friends 0 -1
```

- wir holen die Values in der Liste Friends startend beim Index 0 und enden beim Index -1. In dem Fall holen wir alle Werte.

```bash
lpop friends
```
- löscht das erste Element in der Liste friends

```bash
rpop friends
```
- löscht das letzte Element in der Liste friends

## SET Listen, jeder Value ist unique und ungeordnet

```bash
SADD hobbies "weight lifting"
```
- Hobbies einfügen und den Value dazu
- weil die Werte darin unique sind, kann man den Value nicht mehrfach einfügen

```bash
SMEMBERS hobbies
```
- git den ganzen Inhalt von hobbies aus.

## Hashets

```bash
HSET person name sven
```
- Wir fügen in den key "person" den value "sven" ein.

```bash
HGET person name
```
- Wir holen hier den name aus person

```bash
HGTALL person
```

- Hier holen wir den Key und den Value aus dem Hashset

```bash
HDEL person age
```

- Hier löschen wir das age aus dem key person

```bash
HEXISTS person age
```

- prüfen wir ob der Wert existiert, git 1 zurück bei ja und 0 bei keinen Werten und nll wenn der key nicht existiert