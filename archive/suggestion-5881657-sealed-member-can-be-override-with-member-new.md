# Sealed member can be 'override' with 'member new' keyword like c# [5881657] #

**Submitted by Anonymous on 5/3/2014 12:00:00 AM**  
**1 votes on UserVoice prior to migration**  

C# can do it perfect
public class ObservableBindingDictionary<TKey, TValue> : ObservableDictionary<TKey, TValue>
{
/// <summary>
/// new if for Hide any implementation
/// </summary>
/// <param name="key"></param>
/// <returns></returns>
public new TValue this[TKey key]
{
get
{
if (!base.ContainsKey(key))
{
base.Add(key, default(TValue));
return base[key];
}
else
{
return base[key];
}
}
set
{
if (!base.ContainsKey(key)) //Get和Set的处理都是必要的
{
base.Add(key, value);
}
else if ((base[key]==null && value!=null) || (base[key]!=null && !(base[key].Equals(value))))
{
base[key] = value;
}
}
}
}
F# can do it but with warning message 'This new member hides the abstract member...'
type BindingDictionary<'a,'b when 'a:equality and 'b:equality and 'b:(new:unit->'b)>()=
inherit Generic.Dictionary<'a,'b>()
member this.Item
with get key=
if this.ContainsKey key|>not then base.Add (key,new 'b())
base.[key]
and set key v=
if this.ContainsKey key|>not then base.Add (key,new 'b())
if base.[key]<>v then base.[key]<-v



## Response ##
** by fslang-admin on 2/3/2016 12:00:00 AM **

Declining as this is by design in F#


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5881657)**


## Comments ##

