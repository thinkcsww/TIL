**Android Recycler View**

------

**Why we need recycler View?**

1. It reduces calculation burden. -> Using limited ViewHolder, recycle the viewholders. Otherwise every time a new objects are created, there would be a calculation burden to make a new viewholder everytime.

**First**

As a part of MVC Strategy make a Adapters folder and make a class name like TestAdapter

**Second**

Make a class like below

```
class TestAdapter(val context: Context, val messages: ArrayList<Message>) : RecyclerView.Adapter<TestAdapter.ViewHolder>(){

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        val view = LayoutInflater.from(context).inflate(R.layout.message_list_view, parent, false)
        return ViewHolder(view)
    }

    override fun getItemCount(): Int {
        return messages.count()
    }

    override fun onBindViewHolder(holder: ViewHolder, position: Int) {

        holder.bindMessage(context, messages[position])

    }

    inner class ViewHolder(itemView: View?) : RecyclerView.ViewHolder(itemView) {
        var userImage = itemView?.findViewById<ImageView>(R.id.messageUserImage)
        var timeStamp = itemView?.findViewById<TextView>(R.id.timestampLbl)
        var userName = itemView?.findViewById<TextView>(R.id.messageUserNameLbl)
        var messageBody = itemView?.findViewById<TextView>(R.id.messageBodyLbl)

        fun bindMessage(context: Context, message: Message) {
            val resourceId = context.resources.getIdentifier(message.userAvatar, "drawable", context.packageName)
            userImage?.setImageResource(resourceId)
            userImage?.setBackgroundColor(UserDataService.returnAvatarColor(message.userAvatarColor))
            userName?.text = message.userName
            timeStamp?.text = message.timeStamp
            messageBody?.text = message.message
        }
    }
```



**Third**

```
lateinit var messageAdapter: MessageAdapter
messageAdapter = MessageAdapter(this, MessageService.messages)
messageListView.adapter = messageAdapter

val layoutManager = LinearLayoutManager(this)
messageListView.layoutManager = layoutManager
```

