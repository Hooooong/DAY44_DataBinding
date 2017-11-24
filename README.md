Android Programing
----------------------------------------------------
### 2017.11.23 38일차

#### 예제
____________________________________________________

#### 공부정리
____________________________________________________

##### __DataBinding__

- DataBinding 이란?

  > 데이터 바인딩 라이브러리를 사용하여 선언적 레이아웃을 작성하고, 애플리케이션 로직과 레이아웃을 바인딩하는 데 필요한 글루 코드를 최소화한다.

  - layout 을 작성하면 `findViewById` 를 작성하여 연결해야 하는데, DataBinding 은 그 작업을 최소화 한다.

- DataBinding 사용법

  - Gradle(app) 설정

  ```
  android {
      // 생략
      dataBinding {
          enabled true
      }
  }
  ```

  - layout.xml 설정

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <layout xmlns:android="http://schemas.android.com/apk/res/android">
      <!-- Data Field 추가 -->
      <!-- name : 생성한 객체의 이름, -->
      <!-- Type : 객체의 Package 경로 -->
      <data>
          <variable
            name="user"
            type="com.hooooong.databinding.User"/>
      </data>

      <LinearLayout
          android:orientation="vertical"
          android:layout_width="match_parent"
          android:layout_height="match_parent">

          <!-- 값을 넣는 곳에 @{객체명.변수명} 을 작성한다 -->
          <TextView
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="@{user.id}"/>
          <TextView android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="@{user.name}"/>
      </LinearLayout>
  </layout>
  ```

  - 사용할 객체 설정

  ```java
  // DataBinding 을 사용하기 위해서는
  // POJO 방식 또는 JavaBeans 방식으로 설계한다.

  // @{user.id} 는 getId() 를 호출한다.
  // @{user.name} 은 getName() 을 호출한다.
  public class User {

      private String id;
      private String name;

      public User() {
      }

      public User(String id, String name) {
          this.id = id;
          this.name = name;
      }

      public String getId() {
          return id;
      }

      public void setId(String id) {
          this.id = id;
      }

      public String getName() {
          return name;
      }

      public void setName(String name) {
          this.name = name;
      }
  }
  ```

  - Activit 설정

  ```java
  public class MainActivity extends AppCompatActivity {

      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          // main_activity.xml 의 파일명의 파스칼 표기법으로 Binding 클래스가 생성된다
          // main_activity.xml -> MainActivityBinding
          MainActivityBinding binding = DataBindingUtil.setContentView(this, R.layout.main_activity);
          // binding 객체에 set + xml에 설정한 variable의 name 값을 설정한다.
          // setUser
          // 매개변수에는 xml에 설정한 variable의 package에 있는 객체를 생성하여 추가한다.
          binding.setUser(new User("h921013", "이흥기"));
      }
  }
  ```

- 참고 : [DataBinding](https://developer.android.com/topic/libraries/data-binding/index.html?hl=ko)
