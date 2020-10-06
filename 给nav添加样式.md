# 给nav添加样式

#### SCSS语法
```css
nav{
  display: flex;
  box-shadow: 0 0 3px rgba(0, 0, 0, 0.25);
  font-size: 12px;

  > .item {
    padding: 2px 0;
    width: 33.333%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    .icon{
      width: 32px;
      height: 32px;
    }
  }

  > .item.selected{
    color: #f60;
  }
}
```
#### 去除a标签默认样式
```javascript
a {
  text-decoration: none;
  color: inherit;
}
```
#### 使用active-class
router-link如果被选中，class会添加selected
```vue
<router-link to="/labels" class="item" active-class="selected">
      <icon name="label"/>
      标签
    </router-link>
```
