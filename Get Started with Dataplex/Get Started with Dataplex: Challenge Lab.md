# Get Started with Dataplex: Challenge Lab


## Task 1. Create a lake with a raw zone:

```bash
In the Google Cloud Console, in the Navigation menu (Navigation menu), navigate to Analytics > Dataplex.
or Search Dataplex 
Under Manage Lakes click Mange 
click CREATE lake
Display name: Customer Engagements
region: us-central1
```
It can take up to 3 minutes for the lake to be created.

## Add a zone to the lake:
```bash
On the Manage tab, click on the name of your lake.
Click Add zone.
Display Name: Raw Event Data
Data locations: Regional
Click Create
It can take up to 2 minutes for the zone to be created.
```
Check my progress

## Task 2. Create and attach a Cloud Storage bucket to the zone

```bash
Type: storage bucket
Display name: Raw Event Files
Create a bucket
Name your bucket
continue
Choose where to store your data
Region
select
Done
continue
Inherit
continue
Submit
```
Check my progress

## Task 3. Create and apply a tag template to a zone:

```bash
Under Manage Metadata click tag templates
Click Create tag templates

Protected Raw Data Template
region: us-central1
Visibility: Public
Fields
New Fields
Protected Raw Data Flag
type: Eumerated
values 1: Y
values 2: N
Done
Create
Under Discover click Search
system dataplex click Raw Event Data
attach tag
save 
```

Check my progress

## Congratulations!
