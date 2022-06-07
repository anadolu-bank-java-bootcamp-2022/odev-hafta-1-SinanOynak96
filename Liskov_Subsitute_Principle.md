# The Liskov Substitution Principle

Barbara Liskov tarafından geliştirilen bu prensip kısaca şöyle açıklanabilir:

**Alt sınıflardan oluşturulan nesneler üst sınıfların nesneleriyle yer değiştirdiklerinde aynı davranışı göstermek zorundadırlar.**

Gelin şimdi bu sorunu Liskov’un Yerine Geçme Prensibini uygulayarak çözelim.

Class Diyagramında görüldüğü gibi herşey açık ve net. Tasarımımızı LSP’ye uygun bir vaziyette şekillendirebilmek için gördüğünüz gibi base classtaki tüm işlevler farklı arayüzlere bölmüş bulunmaktayım. Bu yaptığımız işlem bir sonraki yazımda ele alacağım arayüz ayrım prensibinede uyarlı bir yaklaşımdır.

“UcakA”, “UcakB” ve “UcakC” hedefi vurma ve keşif yapma özelliklerine sahip oldukları için iki arayüzden de kalıtım almaktadırlar. “UcakD” ise sadece keşif yapabileceği için sadece “IUcakKesif” arayüzünden kalıtım almaktadır. Bu sayede kullanmayacağı bir işlev olan HedefiVur metodunu barındırmak zorunda kalmayacak ve Dummy Code durumunuda ortadan kaldırmış olacağız

![enter image description here](https://www.gencayyildiz.com/blog/wp-content/uploads/2016/04/Liskovun-Yerine-Ge%C3%A7me-PrensibiLiskov-Substitution-Principle-LSP-2.jpg)

## **Örnek Kod** LSP

    interface IUcakKesif
    
    {
    
    bool KesifYap();
    
    }
    
    interface` IHedefiVur
    
    {
    
    bool HedefiVur();
    
    }
    
    class UcakA : IUcakKesif, IHedefiVur
    
    {
    
    public bool HedefiVur()
    
    {
    
    Console.WriteLine("UcakA Hedefi vurdu.");
    
    return true;
    
    }
    
    public bool KesifYap()
    
    {
    
    Console.WriteLine(``"UcakA keşfi tamamladı."``);
    
    return true;
    
    }
    
    }
    
    class UcakB : IUcakKesif, IHedefiVur
    
    {
    
    public bool HedefiVur()
    
    {
    
    Console.WriteLine("UcakB Hedefi vurdu.");
    
    return true;
    
    }
    
    public bool KesifYap()
    
    {
    
    Console.WriteLine("UcakB keşfi tamamladı.");
    
    return true;
    
    }
    
    }
    
    class UcakC : IUcakKesif, IHedefiVur
    
    {
    
    public bool HedefiVur()
    
    {
    
    Console.WriteLine("UcakC Hedefi vurdu.");
    
    return true;
    
    }
    
    public bool KesifYap()
    
    {
    
    Console.WriteLine("UcakC keşfi tamamladı.");
    
    return true;
    
    }
    
    }
    
    class UcakD : IUcakKesif
    
    {
    
    public bool KesifYap()
    
    {
    
    `Console.WriteLine(``"UcakD keşfi tamamladı."``);`
    
    return true;
    
    }
    
    }
    
    class Savas
    
    {
    
    List<IHedefiVur> HedefVurucular;
    
    List<IUcakKesif> KesifYapicilar;
    
    public Savas(List<IUcakKesif> KesifYapicilar, List<IHedefiVur> HedefVurucular)
    
    {
    
    this.KesifYapicilar = KesifYapicilar;
    
    this.HedefVurucular = HedefVurucular;
    
    }
    
    public void KesifYap()
    
    `{`
    
    KesifYapicilar.ForEach(u =>
    
    {
    
    u.KesifYap();
    
    });
    
    }
    
    public void HedefiVur()
    
    {
    
    HedefVurucular.ForEach(u =>
    
    {
    
    u.HedefiVur();
    
    });
    
    }
    
    }


Gördüğünüz gibi “Savas” sınıfı içerisindeki if – else kontrolüne gerek duymamaktayız.
