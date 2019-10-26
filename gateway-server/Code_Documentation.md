# Directory gateway-server

## app.py
### Function websubmit( )
Handles phone number submission coming from the website
### Function message( )
Callback for Twilio. Messages posted to this route will forward the message
to the Slack channel associated with the senders phone number.
### Function text( )
Callback for Slack. /send commands in Slack will trigger a post to this
route with parameters as defined here:
https://api.slack.com/slash-commands#app_command_handling
### Function assessed( )
Callback for Slack, /assessed commands in Slack will trigger a post to this
route with parameters.
### Function treated( )
Callback for Slack, /treated commands in Slack will trigger a post to this
route with parameters.
### Function need( )
Callback for Slack, /need commands in Slack will trigger a post to this
route with parameters.

The usage for /need is:

/need [name]
ex: /need bed
### Function demographics( )
Callback for Slack, /demographic commands in Slack will trigger a post to this
route with parameters.

The usage for /demographic is:

/demographic [key] [value]
ex: /demographic gender male
### Function event( )
Callback for Slack, /event commands in Slack will trigger a post to this
route with parameters.

The usage for /event is:

/event [name]
ex: /event bed
### Function stage( )
Callback for Slack, /stage commands in Slack will trigger a post to this
route with parameters.

The usage for /stage is:

/stage [stage] [notes]
ex: /stage preparation meeting scheduled with physician
### Function facilities( )
create list of facilities and return
### Function beds( )
Callback for Slack, /beds commands in Slack will trigger a post to this
route with parameters.

The usage for /beds is:

/beds [county] [gender] [age]
ex: /beds philadelphia male 21
### Function aunt_bertha( )
Callback for Slack, /auntbertha commands in Slack will trigger a post to this
route with parameters.

The usage for /211 is:

/auntbertha [zipcode] [keywords]
ex: /auntberta 19107 women recovery
### Function two_one_one( )
Callback for Slack, /211 commands in Slack will trigger a post to this
route with parameters.

The usage for /211 is:

/211 [keyword] [zipcode]
ex: /211 shelter 19011
### Function profiles_index( )
Admin User Interface
Report profiles statistics
### Function profiles_shows( profile_id )
Display rofile message history
### Function profiles_needs_index( )
Display needs
### Function profiles_needs_data( )
Display statistic on needs in counties



## Directory clients

### aunt_bertha.py
#### class AuntBertha
##### Methodearch( self, keywords, zipcode )
Searches Aunt Bertha using the given keyword and zipcode.

Returns a list of 5 dictionaries formatted for Slack attachments

### slack.py

#### Class Team
Teams contain many users contact and availability information.
#### Class Slack
##### Method start_engagement( self, number )
creates group, returning name and number
##### Method forward_twilio_message( self, group, body )
Forwards the body of a twilio message to the channel
##### Method message_to_group( self, body, group_id, attachments=None )
Sends a message to group


### twilio.py
#### Class Twilio
##### Method text( self, number, body="" )
create a message


### two_one_one.py
#### Class TwoOneOne
##### Method search( self, keyword, zipcode )
Searches 211 using the given keyword and zipcode.

Returns a list of 5 dictionaries formatted for Slack attachments


### unomi.py
#### Class Unomi
##### Method create_profile( self, profile_id, properties )
Create a new profile (and session) for a client in Unomi
##### Method update_profile( self, profile_id, properties )
Update profile in Unomi for profile_id
##### Method track_event( self, profile_id, type, properties, user=None )
Tracks and event in unomi.
user == the Slack user recording the event
type == the eventType (e.g. message)
properties == a dictionary of properties to add (e.g. {"text": "Help me"})
##### Method profile_search( self, text )
Fetches a clients profile from Unomi based properties search.
Uses a match all Elasticsearch query to find the profile
##### Method phone_number_from_channel( self, channel )
Fetches a clients phone number from Unomi based on the channel.
The clients profile ID is the same as the channel name.
##### Method channel_from_phone_number( self, phone_number )
Fetches a clients channel (i.e. itemId) from Unomi based on phone number
##### Method list_profiles( self )
Fetches a clients profile from Unomi based properties search.
Uses a match all Elasticsearch query to find the profile
##### list_events( self, profile_id )
Lists all the events for a profile
Uses a match all Elasticsearch query to find the profile

## seeds

### seed.py
#### Function execute( )
Create some number of profiles and fill with data


## utils

### helpers.py
#### Function channel_token( number )
Encodes a phone number to a Slack channel name
of the form is a two word slug. Repeats the same slug for
the same number
#### Function validate_number( number )
Returns a valid phone number or False if number is invalid
#### Function_twilio_number( number )
Validates and formats the number for Twilio
Raises an error for invalid numbers
#### Function return_facilities( zipcode=None )
Returns facilities for a zipcode
#### Function return_beds( county, gender, age )
Looks in the openbeds.csv file and finds any open beds based on
county, gender, and age


### user.py
#### Class User( UserMixin )
##### Method validate( username, password )
check user name and password
