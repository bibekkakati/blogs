## How to store coordinates in MySQL

Many times we [capture the geo-location](https://blog.bibekkakati.me/track-users-location-on-your-website) of users and store in the database for different use cases.
I have seen that most of the developers use multiple fields to store the latitude and longitude separately like
`Table_name(field1, field2, ..., latitude, longitude)`.

In this short article we will see an alternative way of storing coordinates in MySQL database using the spatial data types like `POINT`.

### Create a table

- Let us create a table named `locations`.
- Field `coordinates` of data type `POINT`.

```sql
CREATE TABLE locations (
      id INT(11) NOT NULL AUTO_INCREMENT,
      coordinates POINT,
      PRIMARY KEY (id)
);
``` 

### Insertion of coordinates
- To insert/update the field `coordinates`, we need to prepare a string like this
`'POINT(latitude longitude)'`.
- Then we will use the in-built function called `ST_GeomFromText` to create a geometry in given SRID from [WKT specification](https://dev.mysql.com/doc/refman/8.0/en/gis-wkt-functions.html).
- Pass the prepared string of points into `ST_GeomFromText` function.

```sql
INSERT INTO 
     locations (coordinates) 
VALUES 
     (ST_GeomFromText('POINT(21.67890 91.54789)');
```
Table will store and display the data in the following way

```
id        coordinates
1         POINT(21.67890 91.54789)
```

---

Also, check [this](https://blog.bibekkakati.me/track-users-location-on-your-website) out to know how to capture user's geo-location in web browser.


Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)