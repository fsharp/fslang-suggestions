# Update records to allow embeddable records [13476465] #

**Submitted by Dave Thomas on 4/19/2016 12:00:00 AM**  
**22 votes on UserVoice prior to migration**  

Update the sytax of records to allow the following:
type Position = {X : int; Y : int}
type Sprite = {
Position
Name : string
Image : array byte }
Which would result in the Position records fields being embedded into Sprite.
The Go language has such a feature which works quite nicely:
https://golang.org/ref/spec#Struct_types



**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/13476465)**


## Comments ##


#### Comment by Vasily Kirichenko on 4/19/2016 2:56:00 AM ####
What the construction syntax would look like? In Go it's like this:
type Base struct {
X int
Y int
}
type Foo struct {
Base
Z int
}
func main() {
foo := Foo { Base { 1, 2 }, 3 }
fmt.Println(foo.X + foo.Y + foo.Z)
}


#### Comment by Don Syme on 6/13/2016 5:30:00 AM ####
This looks the same as this suggestion: /archive/suggestion-12879717-allow-record-inheritance-multiple-inheritance


#### Comment by Don Syme on 6/13/2016 5:33:00 AM ####
Oh I see, you mean a sort of mixin of Position into Sprite, e.g. "include Position"
There are zillions of issues associated with this - e.g. what about subtyping? what about members on "Position"? Would Position have to be a struct?
I'd like to see more examples of the utility of this.

