# Project
this project is a concet searching app where user can search for their favorite concert based on price  and genre and the concert matching that criteria is displayed to them and they can chose the one they prefer

# Student ID Number
000904733

# Student Name
Osabuohiense Agho

# Database Setup
this app uses maria db and when populating the detabase i used a scrip file which read the json file directly from my computer using the path of the file, before popu;ating the database i first created the table. below is my script file for populating the detabase

SET @json_data = LOAD_FILE('C:/cprg250s/event.json');

INSERT INTO concerts (ticket_cost, genre, artist, date, time, venue, city, description)
SELECT 
  concert.ticket_cost,
  concert.genre,
  concert.artist,
  concert.date,
  concert.time,
  concert.venue,
  concert.city,
  concert.description
FROM 
  JSON_TABLE(
    @json_data,
    '$[*]' COLUMNS(
      ticket_cost DOUBLE PATH '$.ticket_cost',
      genre VARCHAR(50) PATH '$.genre',
      artist VARCHAR(100) PATH '$.artist',
      date DATE PATH '$.date',
      time TIME PATH '$.time',
      venue VARCHAR(100) PATH '$.venue',
      city VARCHAR(100) PATH '$.city',
      description TEXT PATH '$.description'
    )
  ) AS concert;

