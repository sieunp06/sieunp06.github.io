---
title:  "[☕Java] 접근 제어자(Access Modifier)"
search: false
categories: 
  - Java
tag:
  - 우아한테크코스 프리코스 6기
toc: true
---

> 미루고 미루다 정리하는 접근 제어자

## 접근 제어자(Access Modifier)란?

접근 제어자를 사용하여 변수나 메서드의 사용 권한을 설정할 수 있다.

⇒ **접근 제어자의 종류**

- private
- default
- protected
- public

→ 클래스의 접근 제어자: public, default(생략 가능)

→ 클래스 멤버의 접근 제어자: private, default(생략 가능), protected, public 

`private < default < protecte < public` 순으로 더 많은 접근을 허용한다.

## private

private이 사용된 변수나 메서드는 해당 클래스 안에서만 접근이 가능하다.

```java
public class Sample {
	private String secret;

	private String getSecret() {
		return this.secret;
	}
}
```

⇒ secret 변수와 getSecret 메서드는 Sample 클래스에서만 접근이 가능하며, 다른 클래스에서는 접근할 수 없다.

## default

접근 제어자를 별도로 설정하지 않았다면, default 접근 제어자로 설정된다.

default는 동일한 패키지 안에서만 접근이 가능하다.

**📄 house/HouseKim.java**

```java
package house;

public Class HouseKim {
	String lastname = "Kim";    // default 접근 제어자
}
```

**📄 house/HousePark.java**

```java
package house;

public class HousePark {
	String lastname = "park";

	public static void main(String[] args) {
		HouseKim kim = new HouseKim();
		// HouseKim의 lastname 변수는 default 접근 제어자가 쓰였기 때문에 사용 가능
		System.out.println(kim.lastname);
}
```

## protected

protected는 동일 패키지의 클래스나 해당 클래스를 상속 받은 클래스에서만 접근이 가능하다.

**📄 house/HousePark.java**

```java
package house;

public class HousePark {
	protected String lastname = "park";
}
```

**📄 house/person/SieunPark.java**

```java
package house.person;

import house.HousePark;

public class SieunPark extends HousePark {    // HousePark을 상속함.
	public static void main(String[] args) {
		SieunPark sep = new SieunPark();
		// package가 다르지만, 상속을 받았기 떄문에 접근이 가능하다.
		System.out.println(sep.lastname);   
	}
}
```

## public

public 접근 제어자가 붙었다면 어떤 클래스에서나 접근이 가능하다.

```java
package house;

public class housePark {
	protected String lastname = "park";
	public String info = "this is public message.";
}
```

`info`변수는 public 접근 제어자가 붙었기 때문에 어떤 클래스에서나 접근 가능하다.

```java
import house.HousePark;

public class Sample {
	public static void main(String[] args) {
		HousePark housePark = new HousePark();
		System.out.println(housePark.info);
	}
}
```

## references
- [점프 투 자바 - 접근 제어자](https://wikidocs.net/232)