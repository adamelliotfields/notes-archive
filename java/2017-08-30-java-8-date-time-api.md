# Java 8 Date and Time API
> [`java.time.*`](https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html)

### Class [`DateTimeFormatter`](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html)
The primary class for formatting dates and times. The class contains 15 static constant fields which
can be passed to the format method of other date and time classes.

The `java.time.format` package also includes a `DateTimeFormatterBuilder` class for constructing
complex date-time strings.

### Class [`Instant`](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html)
Represents the start of a nanosecond on the timeline. Instants after the epoch (1/1/1970) are
positive, and instants before are negative.

A `ZonedDateTime` or `OffsetDateTime` object can be converted to an `Instant`; but the reverse is
not true. Converting an `Instant` requires supplying a `ZoneId` or `ZoneOffset`.

```java
Instant.now(); // 2017-08-30T13:44:45.780Z
```

### Class [`LocalDateTime`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html)
Represents a date-time without a time zone in the ISO-8601 calendar system.

To include a time zone, you must use either the `ZonedDateTime` or `OffsetDateTime` class instead.

`LocalDateTime.now()` maps to `TIMESTAMP` in ANSI SQL.

```java
LocalDateTime.now(); // 2017-08-30T13:44:45.809
```

### Class [`OffsetDateTime`](https://docs.oracle.com/javase/8/docs/api/java/time/OffsetDateTime.html)
Represents a date-time with an offset from UTC/Greenwich in the ISO-8601 calendar system.

`OffsetDateTime.now()` maps to `TIMESTAMP WITH TIMEZONE` in ANSI SQL.

```java
OffsetDateTime.now(); // 2017-08-30T13:44:45.810Z
```

### Class [`ZonedDateTime`](https://docs.oracle.com/javase/8/docs/api/java/time/ZonedDateTime.html)
Represents a date-time with a time zone in the ISO-8601 calendar system.

The difference between `OffsetDateTime` and `ZonedDateTime` is that `ZonedDateTime` includes the
rules to account for daylight savings time adjustments.

```java
ZonedDateTime.now(); // 2017-08-30T13:44:45.810Z[Etc/UTC]
```

### Class [`ZoneId`](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneId.html)
A `ZoneId` is used to convert between an `Instant` and a `LocalDateTime`.

A `ZoneId` can be an offset (`-4`), a prefixed offset (`GMT-4`), or a region (`America/New_York`).

### Class [`ZoneOffset`](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneOffset.html)
A `ZoneOffset` is the amount of time that a time zone differs from UTC/Greenwich.

### Examples

```java
String zonedDateTime = ZonedDateTime
                         .now(ZoneId.of("America/New_York"))
                         .format(DateTimeFormatter.RFC_1123_DATE_TIME);
```

```java
String offsetDateTime = OffsetDateTime
                          .now(ZoneOffset.of("-04:00"))
                          .format(DateTimeFormatter.RFC_1123_DATE_TIME);
```

```java
String instantDateTime = Instant
                           .now()
                           .atOffset(ZoneOffset.of("-4"))
                           .format(DateTimeFormatter.RFC_1123_DATE_TIME);
```
