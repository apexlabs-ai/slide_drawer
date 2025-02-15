# SlideDrawer

An easy way to use a drawer with cool sliding animation.

![](example.gif)

## Getting Started

You should add dependency in your flutter project.

```yaml
dependencies:
  slide_drawer: ^1.0.1
```

Or reference the git repo directly:

```yaml
dependencies:
  slide_drawer:
    git: https://github.com/salkuadrat/slide_drawer.git
```

Then run `flutter packages upgrade` or update your packages in IntelliJ.

## Example Project

You can see the `example` folder to learn many different ways you can use SlideDrawer in your app.

## How To Use

As usual, you need to import the package.

```
import 'package:slide_drawer/slide_drawer.dart';
```

Then wrap your app home page with SlideDrawer. 

To use the basic SlideDrawer, you only need to define items (List of MenuItem) to generate menu in your drawer. The drawer will use your default theme color as drawer background, and theme brightness as drawer brightness.

```
class App extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: title,
      // SlideDrawer will use style from this theme
      theme: ThemeData(
        brightness: Brightness.dark,
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      // wrap your HomePage with SlideDrawer
      home: SlideDrawer(
        items: [
          MenuItem('Home', onTap: (){}),
          MenuItem('Project', onTap: (){}),
          MenuItem('Favourite', onTap: (){}),
          MenuItem('Profile', onTap: (){}),
          MenuItem('Setting', onTap: (){}),
        ],
        child: HomePage(),
      ),
    );
  }
}
```

Then you need to set onPressed in your AppBar menu button to toggle SlideDrawer.

```
appBar: AppBar(
  title: Text(title),
  leading: IconButton(
    icon: Icon(Icons.menu),
    // call toggle from SlideDrawer to alternate between open and close
    // when pressed menu button
    onPressed: () => SlideDrawer.of(context).toggle(),
  ),
),
```

### Icons

You can also use icon for your menu items.

```
home: SlideDrawer(
  items: [
    MenuItem('Home', icon: Icons.home, onTap: (){}),
    MenuItem('Project', icon:Icons.rss_feed, onTap: (){}),
    MenuItem('Favourite', icon: Icons.favorite_border, onTap: (){}),
    MenuItem('Profile', icon: Icons.person_outline, onTap: (){}),
    MenuItem('Setting', icon: Icons.settings, onTap: (){}),
  ],
  child: HomePage(),
),
```

### Custom Background

SlideDrawer also come with parameter backgroundColor and backgroundGradient. 

If you specify backgroundGradient, the drawer will use it as background. If not, it will use backgroundColor. If you also not specify backgroundColor, it will use the default theme color as background.

It's good practice to specify brightness (dark or light) if you use backgroundGradient or backgroundColor. 
If you use dark color in your backgroundGradient or backgroundColor, use Brightness.dark.
If you use light color, use Brightness.light.

```
// SlideDrawer with custom gradient as background.
home: SlideDrawer(
  items: [
    MenuItem('Home', icon: Icons.home, onTap: (){}),
    MenuItem('Project', icon:Icons.rss_feed, onTap: (){}),
    MenuItem('Favourite', icon: Icons.favorite_border, onTap: (){}),
    MenuItem('Profile', icon: Icons.person_outline, onTap: (){}),
    MenuItem('Setting', icon: Icons.settings, onTap: (){}),
  ],
  brightness: Brightness.dark,
  backgroundGradient: LinearGradient(
    begin: Alignment.topCenter,
    end: Alignment.bottomCenter,
    stops: [0.0, 1.0], 
    colors: [
      Color(0xFF000046),
      Color(0xFF1CB5E0),
    ],
  ),
  child: HomePage(),
),
```

```
// SlideDrawer with custom color as background.
home: SlideDrawer(
  items: [
    MenuItem('Home', icon: Icons.home, onTap: (){}),
    MenuItem('Project', icon:Icons.rss_feed, onTap: (){}),
    MenuItem('Favourite', icon: Icons.favorite_border, onTap: (){}),
    MenuItem('Profile', icon: Icons.person_outline, onTap: (){}),
    MenuItem('Setting', icon: Icons.settings, onTap: (){}),
  ],
  brightness: Brightness.dark,
  backgroundColor: Colors.blue[900],
  child: HomePage(),
),
```

### Custom Head Drawer

It's advisable to set alignment to SlideDrawerAlignment.start when you use headDrawer.

```
home: SlideDrawer(
  alignment: SlideDrawerAlignment.start,
  headDrawer: Image.asset('boys.png'),
  items: [
    MenuItem('Home', icon: Icons.home, onTap: (){}),
    MenuItem('Project', icon:Icons.rss_feed, onTap: (){}),
    MenuItem('Favourite', icon: Icons.favorite_border, onTap: (){}),
    MenuItem('Profile', icon: Icons.person_outline, onTap: (){}),
    MenuItem('Setting', icon: Icons.settings, onTap: (){}),
  ],
  brightness: Brightness.dark,
  backgroundColor: Colors.blue[900],
  child: HomePage(),
),
```

### Custom Content Drawer

In the previous example, you use items to let the SlideDrawer generate menu in the content drawer.
You can also use any other widget as the content drawer.

```
home: SlideDrawer(
  brightness: Brightness.dark,
  contentDrawer: Container(
    padding: EdgeInsets.symmetric(horizontal: 5),
    child: Column(
      children: [
        ListTile(title: 'Home', icon: Icons.home, onTap: (){}),
        ListTile(title: 'Project', icon:Icons.rss_feed, onTap: (){}),
        ListTile(title: 'Favourite', icon: Icons.favorite_border, onTap: (){}),
        ListTile(title: 'Profile', icon: Icons.person_outline, onTap: (){}),
        ListTile(title: 'Setting', icon: Icons.settings, onTap: (){}),
      ],
    ),
  ),
  child: HomePage(),
),
```

### Custom Full Drawer

If you have your own creative idea for the full widget inside the drawer, don't worry. You can use it too in your SlideDrawer by passing it to drawer. In this way, SlideDrawer will use style of your custom drawer and ignore any value in backgroundColor, gradientColor, and brightness.

```
home: SlideDrawer(
  drawer: Container(
    color: Colors.teal,
    padding: EdgeInsets.symmetric(vertical: 36, horizontal: 15),
    child: Theme(
      data: ThemeData(brightness: Brightness.dark),
      child: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        crossAxisAlignment: CrossAxisAlignment.stretch,
        children: [
          ListTile(title: 'Home', icon: Icons.home, onTap: (){}),
          ListTile(title: 'Project', icon:Icons.rss_feed, onTap: (){}),
          ListTile(title: 'Favourite', icon: Icons.favorite_border, onTap: (){}),
          ListTile(title: 'Profile', icon: Icons.person_outline, onTap: (){}),
          ListTile(title: 'Setting', icon: Icons.settings, onTap: (){}),
        ],
      ),
    ),
  ),
  child: HomePage(),
),
```

### Others

The default SlideDrawer animate your home by move it to the right (offsetFromRight default to 60), scale it, and rotate it at y axis with some small angle (pi / 24 radian or 180 / 24 degree = 7.5 degree). 

If you don't want to rotate, you can disable the rotation by setting isRotate to false.

```
home: SlideDrawer(
  isRotate: false,
  items: [
    MenuItem('Home', icon: Icons.home, onTap: (){}),
    MenuItem('Project', icon:Icons.rss_feed, onTap: (){}),
    MenuItem('Favourite', icon: Icons.favorite_border, onTap: (){}),
    MenuItem('Profile', icon: Icons.person_outline, onTap: (){}),
    MenuItem('Setting', icon: Icons.settings, onTap: (){}),
  ],
  child: HomePage(),
),
```

Or use a custom rotateAngle if you prefer to change the rotation a little bit lower.

```
home: SlideDrawer(
  isRotate: true,
  rotateAngle: pi / 36,
  items: [
    MenuItem('Home', icon: Icons.home, onTap: (){}),
    MenuItem('Project', icon:Icons.rss_feed, onTap: (){}),
    MenuItem('Favourite', icon: Icons.favorite_border, onTap: (){}),
    MenuItem('Profile', icon: Icons.person_outline, onTap: (){}),
    MenuItem('Setting', icon: Icons.settings, onTap: (){}),
  ],
  child: HomePage(),
),
```

Or you can change offsetFromRight to make it move a little closer or farther.
```
home: SlideDrawer(
  offsetFromRight: 80.0,
  items: [
    MenuItem('Home', icon: Icons.home, onTap: (){}),
    MenuItem('Project', icon:Icons.rss_feed, onTap: (){}),
    MenuItem('Favourite', icon: Icons.favorite_border, onTap: (){}),
    MenuItem('Profile', icon: Icons.person_outline, onTap: (){}),
    MenuItem('Setting', icon: Icons.settings, onTap: (){}),
  ],
  child: HomePage(),
),
```

You can also use custom curve and duration if you want. The default values are linear and 300ms. You can also specify curveReverse and durationReverse to change curve and duration of animation in the reverse direction.

```
home: SlideDrawer(
  curve: Curves.easeInOut,
  duration: Duration(milliseconds: 200),
  items: [
    MenuItem('Home', icon: Icons.home, onTap: (){}),
    MenuItem('Project', icon:Icons.rss_feed, onTap: (){}),
    MenuItem('Favourite', icon: Icons.favorite_border, onTap: (){}),
    MenuItem('Profile', icon: Icons.person_outline, onTap: (){}),
    MenuItem('Setting', icon: Icons.settings, onTap: (){}),
  ],
  child: HomePage(),
),
```

There it is. Have fun!!!