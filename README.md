# ![](https://drive.google.com/uc?id=10INx5_pkhMcYRdx_OO4rXNXxcsvPtBYq) 如何在cocos creator使用socket.io (限定v3.0)

<br>

<!--ts-->
## 目錄
* [簡介](#簡介)
* [解決方式](#解決方式)
* [參考資料](#參考資料)
<!--te-->

---
<br>

## 簡介.
在cocos的官方技術文件中有明確的提到，他們只唯一支援websocket，目前也不打算新增支援socket.io，<br>
但是隨著nodejs的技術發展以及使用的人數攀升，相信有不少人都會選擇用Nodejs+Express+Socket.io <br>
來進行與玩家的一個長連接網路應用. 但官方不支援怎麼辦? <br>
其實官方本身也有提到，雖然不支援，但使用者可以自行用第三方的方式進行安裝使用，那具體該怎麼做呢？<br>

> 官方文件中提到：<br>
> Unfortunately, Creator does not provide Socket.io official support on the Web platform,<br>
> requires users to add them themselves to the project.<br> 
> And the Socket.io of the native platform is discarded.<br>
> Previously the socket.io for the native platform was implemented <br>
> by a third-party developer and has not been maintained for a long time.<br>
> So it is not recommended to use.br

---
<br>

## 解決方式
1.首先，我們要先在cocos creator專案中安裝***socket.io-client***
```typescript
npm install socket.io-client
```

<br>

2.在cocos creator的專案中新增ts檔案，這邊我們可以命名成socket.io-client.d.ts***，並且在裡面新增以下代碼.
```typescript
declare module "socket.io-client/dist/socket.io.js" {
    export * from "socket.io-client";
}
```
> 上面的代碼主要是調整指向於套件的位置. <br>
> 當我們在import "socket.io-client" 導入專用於 Node.js 的套件，其主要模塊需要Node.js內置包才能工作。<br>
> 如果要在cocos Creator 中使用它，那我們應該要使用編譯後的版本，<br>
> import io from 'socket.io-client/dist/socket.io.js';<br>

<br>

3. 當上述檔案創建完畢後，即可切回cocos creator，會看見cocos會自動創建meta檔案，好讓專案可以順利的include.<br>
接下來我們就可以直接import使用，如下：
```typescript
import { io } from 'socket.io-client/dist/socket.io.js';
```

<br>

4. import 完之後，接下來就可以直接使用，其用法就跟socket.io的用法一樣，這邊就不多敘述.

<br>

---
<br>

## 參考資料
* [cocos - Standard network interface](https://docs.cocos.com/creator/2.4/manual/en/scripting/network.html) <br>
* [V3.0 and Socket.io-client NPM module](https://discuss.cocos2d-x.org/t/v3-0-and-socket-io-client-npm-module/52910) <br>

---
<!--ts-->
#### [目錄 ↩](#目錄)
<!--te-->
