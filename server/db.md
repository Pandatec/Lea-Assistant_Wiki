## Datastore

The project initially used a GCP Datastore database. It was completely phased out.  
The data itself, was however kept forever.

### Production backup

A backup is available at lea-assistance.appspot.com/backup/3_13_22/3_13_22.overall_export_metadata  
See this link to import: https://console.cloud.google.com/datastore/import?project=lea-assistance

### Staging backup

A backup is available at Lea Google Drive: https://drive.google.com/drive/u/1/folders/1FRTqyDXsVERpv1M6IEyB6_epUVe3nBvx  

- JSON file:  
That is a JSON array with one entry per entity. Extra fields `id` and `kind` (of the respective GCP key) were appended and must be removed on import.  
As of 3/13/2022, there is no implemented mean to import that data.

- Tarball:  
That is a backup of the Docker volume `datastore` at `/opt/data`. To import that data back into a Datastore emulator, see Lea-Server/utils/datastore_emu_backup/restore.sh


## Firestore

Firestore has been transitioned to, and then quickly phased out as well for the cheap Postgres instead.
This database started fresh from scratch. No import was ever performed on it. Please do not consider changing that, all of the Datastore data is probably completely outdated, schema-wise..

## Postgres

This is now the current database type. Everything is strongly typed so that the data finds its way neatly into every column.
See the `server/migrations.md` document to learn how to migrate stuff.
