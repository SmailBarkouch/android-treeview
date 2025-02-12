# android-treeview

[![](https://jitpack.io/v/SmailBarkouch/android-treeview.svg)](https://jitpack.io/#SmailBarkouch/android-treeview)

### Recent changes


Entire library code converted to Kotlin for better stability and reducing null pointer errors though could be used with java as well

2D scrolling mode added, keep in mind this comes with few limitations: you won't be able not place views on right side like alignParentRight. Everything should be align left. Is not enabled by default

### Use in your project

Click [here](https://jitpack.io/#SmailBarkouch/android-treeview) for info on how to use this library in your android application.

### Features
+ 1. N - level expandable/collapsable tree
+ 2. Custom values, views, styles for nodes
+ 3. Save state after rotation
+ 4. Selection mode for nodes
+ 5. Dynamic add/remove node

### Known Limitations
+ For Android 4.0 (+/- nearest version) if you have too deep view hierarchy and with tree its easily possible, your app may crash

<img width='300' hspace='20' align='left' src='https://lh4.ggpht.com/xzkb3N58LH2Tsb_gGs0u3_x81VOLwlhcp-f4pz_sR_iR3vAKXfJoAcwBjN74LvzpVLE=h900-rw' />
<img width='300' hspace='20' src='https://lh5.ggpht.com/Ut6By_iUnkNfzIbaPBsc8hBeQeFj_2UXJh_1tfwDdlTAqGkhiR72A_AwQ0L0GH3OFag=h900-rw' />

### Integration

**1)** Add library as a dependency to your project 

```implementation 'com.github.SmailBarkouch:android-treeview:1.0.0'```

**2)** Create your tree starting from root element. ```TreeNode.root()``` element will not be displayed so it doesn't require anything to be set.
```Kotlin
val root = TreeNode.root()
```

Create and add your nodes (use your custom object as constructor param)
```Kotlin
 val parent = TreeNode("MyParentNode")
 val child0 = TreeNode("ChildNode0")
 val child1 = TreeNode("ChildNode1")
 parent.addChildren(child0, child1)
 root.addChild(parent)
```

**3)** Add tree view to layout
```Kotlin 
 val tView = AndroidTreeView(getActivity(), root)
 containerView.addView(tView.getView())
``` 
The simplest but not styled tree is ready. Now you can see ```parent``` node as root of your tree

**4)** Custom view for nodes

Extend ```TreeNode.BaseNodeViewHolder``` and overwrite ```createNodeView``` method to prepare custom view for node:
```Kotlin
class MyHolder : TreeNode.BaseNodeViewHolder<IconTreeItem> {
    ...
    override fun createNodeView(val node, val value) : View?{
        val inflater = LayoutInflater?.from(context)
        val view = inflater?.inflate(R.layout.layout_profile_node, container, false)
        val tvValue = view?.findViewById(R.id.node_value) as? TextView
        tvValue.setText(value.text)
        
        return view
    }
    ...
    class IconTreeItem {
        val icon
        val text
    }
}
```

**5)** Connect view holder with node 
```Kotlin 
  val nodeItem = IconTreeItem()
  val child1 = TreeNode(nodeItem).setViewHolder(new MyHolder(mContext))
```

**6)** Consider using 
```Kotlin 
TreeNode.setClickListener(TreeNodeClickListener listener)
AndroidTreeView.setDefaultViewHolder
AndroidTreeView.setDefaultNodeClickListener
...
```
