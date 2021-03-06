Example technique for retrieving all hashes with a given tag from ThreatExchange.

# Purpose of this code

You can use this for downloading hashes from ThreatExchange, found by tag. You can use the Java code as-is, or use it to illuminate tooling in other languages. Note that `java TETagQuery -s ...` will print the URLs this tool constructs for you, to help make clear how to access ThreatExchange via URLs.

# Query mechanism

* We use the `tagged_objects` endpoint to fetch IDs of all hashes. This
endpoint doesn't return all desired metadata fields, so we use it as a quick
map from tag ID to list of hash IDs. This is relatively quick.

* Then for each resulting hash ID we do a query for all fields associated with
that ID. This is relatively slow, but batching multiple IDs per query helps a
lot.

# Compiling the code

```
javac TETagQuery.java
```

# Running the code

Examples:

```
java TETagQuery --help
java TETagQuery --pdq -q tag-to-details media_type_photo
java TETagQuery --photodna -q tag-to-details media_type_photo
java TETagQuery --md5 tag-to-details media_type_video
java TETagQuery tag-to-details --page-size 10 --hash-dir ./tmk-hash-dir --hash-type tmk media_priority_test
```

# Contact

threatexchange@fb.com
