<br/>

# Kalıtım (Inheritance) Yerine Bileşim Tercih Edin

Nesne-yönelimli programlamada (OOP) bileşim (composition), daha basit nesneleri veya bileşenleri birleştirerek karmaşık nesneler oluşturmak için kalıtıma (inheritance) bir alternatiftir. Bileşim (Composition), geleneksel kalıtıma (inheritance) kıyasla kodun yeniden kullanılabilirliğini, esnekliğini ve daha modüler bir tasarımı destekler. Typescript'te, bileşimi (composition) çeşitli şekillerde kullanabilirsiniz ve her biri için örnekler vereceğim.

<br/>

---

<br/>

### Örnek 1: Basit Bileşim — Simple Composition

Job bileşenine sahip bir Person sınıfı oluşturmak istediğimizi varsayalım.
Kalıtım (Inheritance) kullanmak yerine Bileşim (Composition) kullanacağız.

```tsx
class Job {
  constructor(private title: string, private salary: number) {}

  getDetails() {
    return `${this.title} - Salary: $${this.salary}`;
  }
}

class Person {
  constructor(private name: string, private age: number, private job: Job) {}

  info() {
    return `Hi, I'm ${this.name}, ${
      this.age
    } years old. ${this.job.getDetails()}`;
  }
}

const softwareEngineer = new Job("Software Developer", 10000);
const person = new Person("Alice", 27, softwareEngineer);

console.log(person.info());
```

Bu örnekte, bir Job sınıfı ve Job sınıfının bir örneğini içeren bir Person sınıfı oluşturduk. Bu basit bir bileşim (composition) örneğidir.

<br/>

---

<br/>

### Örnek 2: Arayüzleri Kullanmak — Use Interfaces

Oluşturulan bileşenler (components) için belirli bir yapıyı zorunlu kılmak üzere arayüzleri (interfaces) de kullanabilirsiniz:

```tsx
interface Engine {
  start(): void;
  stop(): void;
}

class ElectricEngine implements Engine {
  start() {
    console.log("Electric engine started.");
  }

  stop() {
    console.log("Electric engine stopped.");
  }
}

class Car {
  constructor(
    private make: string,
    private model: string,
    private engine: Engine
  ) {}

  drive() {
    console.log(`Driving a ${this.make} ${this.model}`);
    this.engine.start();
  }

  stop() {
    this.engine.stop();
  }
}

const electricEngine = new ElectricEngine();
const tesla = new Car("Tesla", "Model 3", electricEngine);

tesla.drive();
tesla.stop();
```

Bu örnekte, bir Engine arayüzüne sahibiz ve Car sınıfı, Engine arayüzünü uygulayarak farklı motor türlerini (örneğin, elektrikli, benzinli) birleştirmek için bileşimi (composition) kullanır.

<br/>

---

<br/>

### Örnek 3: Dinamik Bileşim — Dynamic Composition

Bileşim (Composition), bileşenleri dinamik olarak değiştirmenize olanak tanıyarak kodunuzu daha esnek hale getirir:

```tsx
class Camera {
  takePhoto() {
    console.log("Taking a photo");
  }
}

class MusicPlayer {
  playMusic() {
    console.log("Playing music");
  }
}

class Smartphone {
  private camera: Camera | null;
  private musicPlayer: MusicPlayer | null;

  attachCamera(camera: Camera) {
    this.camera = camera;
  }

  attachMusicPlayer(player: MusicPlayer) {
    this.musicPlayer = player;
  }

  useCamera() {
    if (this.camera) {
      this.camera.takePhoto();
    } else {
      console.log("No camera attached.");
    }
  }

  useMusicPlayer() {
    if (this.musicPlayer) {
      this.musicPlayer.playMusic();
    } else {
      console.log("No music player attached.");
    }
  }
}

const smartphone = new Smartphone();
smartphone.useCamera(); // Output: No camera attached.
smartphone.useMusicPlayer(); // Output: No music player attached.

const camera = new Camera();
const musicPlayer = new MusicPlayer();

smartphone.attachCamera(camera);
smartphone.attachMusicPlayer(musicPlayer);

smartphone.useCamera(); // Output: Taking a photo
smartphone.useMusicPlayer(); // Output: Playing music
```

Bu örnekte Smartphone sınıfı, bileşenleri (camera ve music player) dinamik olarak eklemenize ve çıkarmanıza olanak tanır.

<br/>

Bu örnekler, Typescript'teki bileşimin (composition), kalıtıma (inheritance) dayanmadan esnek ve yeniden kullanılabilir yazılım bileşenleri oluşturmanıza nasıl olanak sağladığını göstermektedir. Daha modüler ve bakımı kolay bir kod tabanını destekler.

---

— Taner Çeker tarafından hazırlanmıştır.
