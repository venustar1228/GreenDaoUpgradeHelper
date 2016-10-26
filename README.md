# GreenDaoUpgradeHelper([中文版](./README_CH.md))

[![Release](https://jitpack.io/v/yuweiguocn/GreenDaoUpgradeHelper.svg)](https://jitpack.io/#yuweiguocn/GreenDaoUpgradeHelper)

GreenDaoUpgradeHelper is a database upgrade helper for greenDao.Use GreenDaoUpgradeHelper can easy solve database upgrade that's just need one line code.



##How to use
1.Add it in your root build.gradle at the end of repositories:
```
	allprojects {
		repositories {
			...
			maven { url "https://jitpack.io" }
		}
	}
```

2.Add the dependency（greendao 3.0 above）
```
	dependencies {
	        compile 'org.greenrobot:greendao:3.2.0'
	        compile 'com.github.yuweiguocn:GreenDaoUpgradeHelper:v1.1.0'
	}
```
or (greendao 3.0 below)
```
    dependencies {
            compile 'de.greenrobot:greendao:2.0.0'
	        compile 'com.github.yuweiguocn:GreenDaoUpgradeHelper:v1.0.1'
	}
```

3.Add a new class that extends **DaoMaster.OpenHelper**,add a constructor,implement **onUpgrade** method and called **migrate** method,arguments is all of generated Dao class:

```
MigrationHelper.migrate(db,TestDataDao.class,TestData2Dao.class,TestData3Dao.class);
```


like this:  
```
public class MySQLiteOpenHelper extends DaoMaster.OpenHelper {
    public MySQLiteOpenHelper(Context context, String name, SQLiteDatabase.CursorFactory factory) {
        super(context, name, factory);
    }
    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        MigrationHelper.migrate(db,TestDataDao.class,TestData2Dao.class,TestData3Dao.class);
    }
}

```  

4.Finally,init like this:

```
//MigrationHelper.DEBUG = true;  //if you want see the log info,default is false
MySQLiteOpenHelper helper = new MySQLiteOpenHelper(this, "test.db",
                null);
        daoMaster = new DaoMaster(helper.getWritableDatabase());
```


##Thanks
[greenDAO](https://github.com/greenrobot/greenDAO)


##Contact me
weibo:[@于卫国](http://weibo.com/weiguo58)

gmail:[yuweiguocn@gmail.com](mailto:yuweiguocn@gmail.com)

blog:[yuweiguo's blog](http://yuweiguocn.github.io)

##License
```
Copyright 2016 yuweiguocn

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
