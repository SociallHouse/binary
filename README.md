## binary

Сериализация примитивных типов в набор байтов для последующей отправки по сети

-------

## Examples

```go
package main

import "github.com/Sociall-House/binary" 

func main(){
    // int + byte + byte array
    w := binary.AcquireWriter(4 + 1 + 5)
    w.WriteSignedInt32(5835)
    w.WriteByte(124)
    w.WriteByteArray(4, []byte{ 0xAA, 0xBB, 0xCC, 0xDD })
    
    sendToServer(w.Buffer())

    
}

func sendToServer(buf []byte){
    
}
```

```go
package main

import "github.com/Sociall-House/binary" 

func main(){
    r := binary.AcquireReader(getBytesFromServer())

    someInt, err := r.ReadSignedInt32()
    checkErr(err)

    someByte, err := r.ReadByte()
    checkErr(err)

    someByteArrayLen, someByteArray, err := r.ReadByteArray()
    checkErr(err)

    doSomething(someInt, someByte, someByteArrayLen, someByteArray)
}

func checkErr(err error){

}

func getBytesFromServer() ([]byte, int){
    return []byte{ 0x11, 0x22, 0x33, 0x44, 0x55, 0x04, 0x77, 0x88, 0x99, 0xAA }, 10
}

func doSomething(someInt int32, someByte byte, someByteArrayLen byte, someByteArray []byte){

}
```