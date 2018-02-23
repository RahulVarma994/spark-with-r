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

# Manipulate the track metadata
track_metadata_tbl %>% select("artist_name","release", "title","year")
 
# Try to select columns using [ ]
tryCatch({
    # Selection code here
    track_metadata_tbl[, c("artist_name", "release", "title", "year")]
  },
  error = print

# Disconnect from Spark
spark_disconnect(sc = spark_conn)
