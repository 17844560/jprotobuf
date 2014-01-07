jprotobuf
=========

A very useful utility library for java programmer using google protobuf<br>
jprotobuf�����Java���򿪷�һ�׼�����⣬Ŀ���Ǽ�java���Զ�protobuf����ʹ��<br>
ʹ��jprotobuf����������ȥ�˽�.proto�ļ��������﷨��ֱ��ʹ��javaע�ⶨ���ֶ����ͼ��ɡ�

## ����Ҫ�� ##
JDK 6 �����ϰ汾

## APIʹ��˵�� ##

ʾ����������Ҫ����protobuf����һ�����ݽӿڣ������������ԣ�һ����string��һ����int32

### ��ͳprotobufʹ�ù��� ###

a ����.proto˵���ļ�. test.proto

```property
package pkg;  

option java_package = "com.baidu.bjf.remoting.protobuf";
  
//�������������java������  
option java_outer_classname = "SimpleTypeTest";  
  
message InterClassName {  
  required string name = 1;
  required int32  value = 2; 
}  
  
```

b ʹ��protoc.exe ����.proto�ļ�
```cmd
 protoc --java_out=src  test.proto
``` 

c �������ɵ�Java�ļ�������protobuf API�������л��뷴�򻯲���<br>
���л�������
```java
InterClassName icn = InterClassName.newBuilder().setName("abc")
		.setValue(100).build();
		
		byte[] bb = icn.toByteArray();
``` 

���򻯲���<br>
```java
byte[] bb = ...;
InterClassName icn = InterClassName.parseFrom(bb);
``` 


### ʹ��jprotobuf API �򻯿��� ###
a ʹ��ע��ֱ��ʹ��pojo����

```java
import com.baidu.bjf.remoting.protobuf.FieldType;
import com.baidu.bjf.remoting.protobuf.annotation.Protobuf;


/**
 * A simple jprotobuf pojo class just for demo.
 * 
 * @author xiemalin
 * @since 1.0.0
 */
public class SimpleTypeTest {

    @Protobuf(fieldType = FieldType.STRING, order = 1, required = true)
    private String name;
    
    @Protobuf(fieldType = FieldType.INT32, order = 2, required = false)
    private int value;

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }
    
}
``` 

b ʹ��jprotobuf API�������л��뷴���л�����
```java
        Codec<SimpleTypeTest> simpleTypeCodec = ProtobufProxy
                .create(SimpleTypeTest.class);

        SimpleTypeTest stt = new SimpleTypeTest();
        stt.name = "abc";
        stt.setValue(100);
        try {
            // ���л�
            byte[] bb = simpleTypeCodec.encode(stt);
            // �����л�
            SimpleTypeTest newStt = simpleTypeCodec.decode(bb);
        } catch (IOException e) {
            e.printStackTrace();
        }

``` 
## ��ϵ���� ##

email: [rigelarch_sh@baidu.com](mailto://email:rigelarch_sh@baidu.com "���ʼ���jprotobuf������")


