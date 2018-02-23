# spark-with-r
install sparklyr package 
# Load sparklyr
library(sparklyr)
# Connect to your Spark cluster
spark_conn = spark_connect(master = "local")
# Print the version of Spark
spark_version(sc = spark_conn)
#Explore track_metadata structure
str(track_metadata)
# Copy track_metadata to Spark
track_metadata_tbl <- copy_to(spark_conn, track_metadata)
# track_metadata_tbl has been pre-defined
track_metadata_tbl
# Print 5 rows, all columns
print(track_metadata_tbl, n = 5, width = Inf)

# Examine structure of tibble
str(track_metadata_tbl)
# Examine structure of data
glimpse(track_metadata_tbl)
# Manipulate the track metadata
track_metadata_tbl %>% select("artist_name","release", "title","year")
 
# Try to select columns using [ ]
tryCatch({
    # Selection code here
    track_metadata_tbl[, c("artist_name", "release", "title", "year")]
  },
  error = print
# Manipulate the track metadata
track_metadata_tbl %>%select(artist_name,release, title,year)%>%filter(year >= 1960 , year < 1970)%>%arrange(artist_name, desc(year),  title)
# Manipulate the track metadata
track_metadata_tbl %>%select(title, duration) %>%
  # Mutate columns
  mutate(duration_minutes = duration / 60)
  
   # Select columns starting with artist
  select(starts_with("artist"))


  # Select columns ending with id
  select(ends_with("id"))

# Disconnect from Spark
spark_disconnect(sc = spark_conn)
