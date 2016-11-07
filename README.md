# hw3ndb
These are the changes I've made to Udacity's Intro to Backend hw3 so that it uses ndb instead of db.

1 from google.appengine.ext import ndb 
          to

from google.appengine.ext import ndb

2 

class Post(db.Model):
    subject = db.StringProperty(required = True)
    content = db.TextProperty(required = True)
    created = db.DateTimeProperty(auto_now_add = True)
    last_modified = db.DateTimeProperty(auto_now = True)
    
            to

class Post(ndb.Model):
    subject = ndb.StringProperty(required = True)
    content = ndb.TextProperty(required = True)
    created = ndb.DateTimeProperty(auto_now_add = True)
    last_modified = ndb.DateTimeProperty(auto_now = True)
    
3  

posts = db.GqlQuery("select * from Post order by created desc limit 10")

                       to

posts = ndb.gql("select * from Post order by created desc limit 10")


4 return db.Key.from_path('blogs', name)  

        to

return ndb.Key('blogs', name)

5 post = db.get(key)  

        to
        
post = key.get()

6 key = db.Key.from_path('Post', int(post_id), parent=blog_key())   

                  to

key = ndb.Key('Post', int(post_id), parent=blog_key())

7  

 self.redirect('/blog/%s' % str(p.key().id()))

 to  
 
 self.redirect('/blog/%s' % str(p.key.integer_id()))
