Navigaion 컴포넌트
==========================================
Stack, Drawer, BottomTab 내비게이션
------------------------------------------

### 내비게이션 함수 호출
```
const Stack = ceateStackNavigator();
const BottomTab = createBottomTabNavigator();
const Drawer = createDrawerNavigator();
```

* 화면에 내비게이션 헤더가 필요한 경우, 스택 내비게이션을 추가
### 1. Loginnavigator
```
const LoginNavigator = () => {
    return (
        <Stack.Navigator screenOptions-{{headerShown : false}}>
            <Stack.Screen name="Login" component={Login}>
            <Stack.Screen name="SignUp" component={SignUp}>
            <Stack.Screen name="PsswordReset" component={PsswordReset}>
        </Stack.Navigator>
    );
};
```

### 2. MyFeedTab
```
const MyFeedTab = () => {
    return (
        <Stack.Navigator>
            <Stack.Screen
                name="Feeds"
                component="Feeds"
                options={{ title : 'SNS App' }}
            />
        </Stack.Navigator>
    );
};
```
### 3. FeedTabs
```
const FeedsTab = () => {
    return (
        <Stack.Navigator>
            <Stack.Screen
                name="Feeds"
                component={Feeds}
                options={{
                    header : () => <SearchBar />
                }}
            />

            <Stack.Screen
                name="FeedListOnly"
                component={FeedListOnly}
                options={{
                    headerBackTitleVisible : false,
                    title : '둘러보기',
                    headerTintColor : '#292929',
                }}
            />
        </Stack.Navigator>
    );
};
```

### 4. UploadTab
```
const UploadTab = () => {
    return (
        <Stack.Navigator>
            <Stack.Screen
                name="Upload"
                component="{Upload}
                options={{
                    title : '사진 업로드'
                }}
            />
        <Stack.Navigator>
    );
};
```

### 5. ProfileTab
```
const ProfileTab = () => {
    return (
        <Stack.Navigator>
            <Stack.Screen
                name="Profile"
                component={Profile}
                options={{title : 'Profile'}}
            />
        </Stack.Navigator>
    );
};
```

### 6. MainTab : 각각의 컴포넌트에 명시 된 것들이 위의 코드들에 해당
```
const MainTabs = () => {
    return (
        <BottomTab.Navigator tabBarOptions={{showLabel : false}}>
            <BottomTab.Screen
                name="MyFeed"
                component={MyFeedTab}
                options={{
                    tabBarIcon : ({color, focused}) => (
                        <Image
                            source = {
                                focused
                                    ? require('~/Aseets/Images/Tabs/ic_home.png')
                                    : require('~/Aseets/Images/Tabs/ic_home_outline.png')
                            }
                        />
                    )
                }}
            />

            <BottomTab.Screen
                name="Feeds"
                component={FeedsTab}
                options={{
                    tabBarIcon : ({color, focused}) => (
                        <Image
                            source = {
                                focused
                                    ? require('~/Aseets/Images/Tabs/ic_search.png')
                                    : require('~/Aseets/Images/Tabs/ic_search_outline.png')
                            }
                        />
                    )
                }}
            />

            <BottomTab.Screen
                name="Upload"
                component={UploadTab}
                options={{
                    tabBarLabel : 'Third',
                    tabBarIcon : ({color, focused}) => (
                        <Image
                            source = {
                                focused
                                    ? require('~/Aseets/Images/Tabs/ic_add.png')
                                    : require('~/Aseets/Images/Tabs/ic_add_outline.png')
                            }
                        />
                    )
                }}
            />

            <BottomTab.Screen
                name="Notification"
                component={Notification}
                options={{
                    tabBarIcon : ({color, focused}) => (
                        <Image
                            source = {
                                focused
                                    ? require('~/Aseets/Images/Tabs/ic_favorite.png')
                                    : require('~/Aseets/Images/Tabs/ic_favorite_outline.png')
                            }
                        />
                    )
                }}
            />

            <BottomTab.Screen
                name="Profile"
                component={ProfileTab}
                options={{
                    tabBarIcon : ({color, focused}) => (
                        <Image
                            source = {
                                focused
                                    ? require('~/Aseets/Images/Tabs/ic_profile.png')
                                    : require('~/Aseets/Images/Tabs/ic_profile_outline.png')
                            }
                        />
                    )
                }}
            />
        </BottomTab.Navigator>
    );
};
```

### 7.  MainNavigator : Drawer 내비게이터 사용
```
const MainNavigator = () => {
    return (
        <Drawer.Navigator
            drawerPosition="right" {/* 내비게이션 위치/}
            drawerType="slide"
            drawerContent={(props) => <CustomDrawer props={props} />}>
                <Drawoer.Screen name="MainTabs" component={MainTabs} />
        <Drawer.Navigator/>
    );
};

export deafalut () => {
    / 로그인 여부 확인 */
    const { isLoading, userInfo } = useContext<IUserContext>(UserContext);

    if(isLoading === false) {
        return <Loading />;
    }

    return (
        <Navigaioncontainer>
            {userInfo ? <MainNavigator /> : <LoginNavigator />}
        </Navigaioncontainer>
    )
}
```

## 내비게이션 적용
  * App.tsx 수정
  * 타입스크립트 사용 시
  ```
  import React form 'react';
  import { StatusBar } from 'react-native';

  import Navigator from '~/Screens/Navigator';
  import { UserContextProvider } from '~/Context/User';
  import { RandomUserDataProvider } from '~/Context/RandomUserData';

  interface Props {}

  const App = ({} : Props) {
      return (
          <RandomUserDataProvider cache={true}>
            <UserContextProvider>
                <StatusBar barStyle="default" />
                <Navigator />
            </UserContextProvider>
          </RandomUserDataProvider>
      );
  };

  export default App;
  ```