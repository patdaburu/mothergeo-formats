# ![Img](https://raw.githubusercontent.com/patdaburu/mothergeo-assets/master/images/png/48/logo.png "MotherGeo Logo") MotherGeo Formats

## Overview

This project contains schema descriptions for the MotherGeo project.

## Format Documents

### `model.json`

A `model.json` file describes a data model as well as explicit contracts between data providers and data consumers.  As the file extension suggests, it is expressed in [Javascript Object Notation (JSON)](<http://www.json.org/>) as a single JSON object.  This section details the document structure.

While you're waiting for MotherGeo to provide model development tools, you can inspect existing model documents using one of the many free [JSON editors](<http://www.jsoneditoronline.org/>) that can be found online.

### General Structure

This section defines the general structure of the *Model* object defined in a `model.json` file.

* __name__ : human-readable name for the model

* __revision__ : publication information
    * __title__ : human-readable identification of the specific revision
    * __sequence__ : increments with each new revision and can be used to determine if one version of the model is more recent than another
    * __authorName__ : the revision's author
    * __authorEmail__ : the email address of the revision's author
    
* __spatial__ : information pertaining to spatial portions of the model (*e.g.* featureclasses)
    * __commonSrid__ : the common [spatial reference ID (SRID)](<https://en.wikipedia.org/wiki/Spatial_reference_system>) for all spatial data
    * __commonFields[]__ : definitions of [fields](#field) common to every [featureclass](#featureclass)
    * __featureClasses__ : definitions of [featureclasses](#featureclass) included in the model
    
### Field

*Field* objects define fields (*a.k.a.* columns, attributes, *etc*) in tables and featureclasses.

* __name__ : the *actual* name of the field as it will appear in the `Mother` database
* __type__ : the data type
    * *guid* : a [globally unique identifier](<https://betterexplained.com/articles/the-quick-guide-to-guids/>)
    * *text* : strings of text
    * *int* : a whole number
    * *float* : a floating-point number
    * *datetime* : a moment in time
* __width__ : indicates the size of the field and applies only to *text* types
* __domain__ : constrains the allowed values in a field to a list
* __source__ : contracts with source data providers
    * __requirement__ : the requirement upon the source data to provide the data in this field
        * *null* or *none* : the source data is neither required, nor requested, to provide this data field
        * *requested* : the source data may, optionally, provide this data field
        * *required* : the source data *must* provide this data field
    * __requested__ : the source data provider is invited to provide the data that will appear in this field
    * __required__ : the source data provider *must* provide the data that will appear in this field
* __target__ : contracts with the target data consumer and advice to `Mother` to be used during processing
    * __calculated__ : the value in this field is calculated
    * __guaranteed__ : this field is guaranteed to have a non-empty value
* __usage__ : indicates how the data in this field is intended to be used
    * __search__ : the data in this field may be used to find a row
    * __display__ : the data in this field may be used to display information about a row
* __nena__ : [NENA specification] information as defined by a [nena](#nena) object.
* __i18n__ : internationalized label information; each supported language is identified by its ISO code and defined by an [i18n](#i18n) object.

### FeatureClass

*Featureclasses* objects define collections of spatial objects that share a common geometry type and common attribution.

* __name__ : the *actual* name of the featureclass as it appears in a `Mother` database
* __geometryType__ : the type of the geometry contained in the featureclass
    * *Point* : a point geometry
    * *Polyline* : a polyline geometry
    * *Polygon* : a polygon geometry
* __nena__ : [NENA specification] information as defined by a [nena](#nena) object.
* __i18n__ : internationalized label information; each supported language is identified by its ISO code and defined by an [i18n](#i18n) object.
* __fields[]__ : definitions of [fields](#field) defined for this featureclass

### Nena

*Nena* objects indicate how another object definition relates to the general NENA specification.

* __nena__ : describes how this field relates to a field described in the NENA specification
    * __analog__ : the analogous NENA field or table name
    * __required__ : indicates whether or not the NENA specification requires this field to contain a non-empty value
    
### I18n

*I18n* objects provide human-readable descriptions of other objects in the various supported languages.

* __friendlyName__: human-readable identifier
* __description__: human-readable description


### Supported Models 

* __GeoComm__
A `Mother` model that conforms to [GeoComm's published *Unified Data Model*](./geocomm/model.json) is currently in development.



  




