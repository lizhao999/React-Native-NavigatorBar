#使用说明

此module是依据`react-native-navbar` 进行开发的

因为`navbar`  `title` `leftNavBar` `rightNavBar` 不支持图片作为图标去使用

###使用方法
--
```
var rightButtonConfig = {
            title: 'Next',
            handler: function onNext() {
                alert('hello!');
            }
        };
        var leftButtonConfig = {
            // title:'Back',
            titleView:<Icon name={ 'ios-settings' } size={30} color={'#4E78E7'}/>,
            handler: function onNext() {
                alert('hello!');
            }
        };
        var titleConfig = {
            // title: 'Hello, world',
            //titleView:<Icon name={ 'ios-settings' } size={30} color={'#4E78E7'}/>
            titleView:
                    <View style={{width: 150, height: 40}}>
                        <Image source={{uri: 'https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=4091185693,1767337066&fm=23&gp=0.jpg'}}
                               style={{width: 150, height: 40}}
                        />
                    </View>
        };
        var statusBarConfig = {
            // hidden: 'false',
            // tintColor:'red',
            // hideAnimation:'slide'
        };
```
`title` `titleView` 二者只能设置一个 `title` 优先于`titleView`

`titleView` 可以为Icon,Image,View,等  属性为any.

###修改的代码
```
index.js
const ButtonShape = {
  //去除isRequired 		
  title: PropTypes.string,
  style: PropTypes.any,
  handler: PropTypes.func,
  disabled: PropTypes.bool,
  //增加titleView  为any属性
  titleView: PropTypes.any,
};
```
--
修改getTitleElement(data) 方法（此方法为设置title方法, leftNavBar类似）
--
```
 renderView(data) {
    const colorStyle = data.tintColor ? {color: data.tintColor,} : null;
    if (data.title) {
      return <Text
          style={[styles.navBarTitleText, colorStyle,]}>
        {data.title}
      </Text>
    } else {
      return data.titleView
      }}getTitleElement(data) {
    if (!!data.props) {
      return <View style={styles.customTitle}>{data}</View>;
    }
    return (
      <View style={styles.navBarTitleContainer}>
        {this.renderView(data)}
      </View>
    );
    }
```




