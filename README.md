# **۱۷ سوال مصاحبه ری‌اکت که هر توسعه‌دهنده‌ای در سال ۱۴۰۴ باید بداند**  
<div dir="rtl" style="text-align: right;">

ری‌اکت یکی از **پرتقاضاترین مهارت‌ها** برای توسعه‌دهندگان فرانت‌اند در سال است. اگر برای **مصاحبه توسعه‌دهندگی ری‌اکت** آماده می‌شوید، بسیار مهم است که با **بهترین شیوه‌ها، الگوها و مفاهیم به‌روز** پیش بروید.  

این مقاله لیستی از **۱۷ سوال مصاحبه ری‌اکت** را گردآوری کرده که همه چیز را از **اصول پایه** تا **بهینه‌سازی‌های پیشرفته** عملکرد پوشش می‌دهد و به شما کمک می‌کند در **مصاحبه بعدی خود بدرخشید**.  

**بیایید شروع کنیم!**  

---

## **۱. DOM مجازی در ری‌اکت چیست؟ چه تفاوتی با DOM واقعی و Shadow DOM دارد؟**  

**DOM مجازی** مفهومی است که در آن یک نمایش مجازی از DOM واقعی در حافظه نگهداری می‌شود و فقط در صورت لزوم توسط کتابخانه‌ای مانند `ReactDOM` با DOM واقعی همگام‌سازی می‌شود.  

✅ **مزایا:**  
- **بهبود عملکرد** (فقط بخش‌های تغییرکرده به‌روز می‌شوند).  
- **کاهش دستکاری مستقیم DOM** (کاهش هزینه‌های رندر).  

❌ **تفاوت با DOM واقعی و Shadow DOM:**  
| **DOM مجازی** | **DOM واقعی** | **Shadow DOM** |  
|--------------|-------------|--------------|  
| نمایش مجازی در حافظه | ساختار واقعی HTML در مرورگر | محیط ایزوله برای کامپوننت‌های وب |  
| توسط ری‌اکت مدیریت می‌شود | مستقیماً توسط مرورگر پردازش می‌شود | برای کپسوله‌سازی استایل و منطق استفاده می‌شود |  

---

## **۲. دو نوع کامپوننت در ری‌اکت کدامند؟ و چه زمانی باید از آنها استفاده کنیم؟**  

دو نوع کامپوننت در ری‌اکت وجود دارد:  

1. **کامپوننت‌های کلاسی** (`Class Components`)  
2. **کامپوننت‌های تابعی** (`Functional Components`)  

### **مقایسه:**  
| **کامپوننت‌های کلاسی** | **کامپوننت‌های تابعی** |  
|----------------------|----------------------|  
| از `this.state` و `this.props` استفاده می‌کنند | از هوک‌ها (`useState`, `useEffect`) استفاده می‌کنند |  
| دارای متدهای چرخه حیات (`componentDidMount`, ...) | چرخه حیات با `useEffect` مدیریت می‌شود |  
| سنگین‌تر و پیچیده‌تر | سبک‌تر و خوانا‌تر |  

🔹 **پیشنهاد:**  
- **از کامپوننت‌های تابعی استفاده کنید** (مگر در موارد خاص مثل `Error Boundaries`).  

---

## **۳. چرا در ری‌اکت به `key` نیاز داریم؟**  

`key` به ری‌اکت کمک می‌کند **عناصر منحصربه‌فرد** را در لیست‌ها شناسایی کند و از **بازسازی غیرضروری DOM** جلوگیری کند.  

❌ **بدون `key`:**  
```jsx
{todos.map((todo) => (
  <li>{todo.text}</li> // هر بار کل لیست بازسازی می‌شود!
))}
```  

✅ **با `key`:**  
```jsx
{todos.map((todo) => (
  <li key={todo.id}>{todo.text}</li> // فقط آیتم‌های تغییرکرده به‌روز می‌شوند
))}
```  

⚠️ **هشدار:**  
- **از `index` به عنوان `key` استفاده نکنید** (مگر در لیست‌های ایستا).  

---

## **۴. تفاوت بین `input` کنترل‌شده و کنترل‌نشده در ری‌اکت چیست؟**  

| **کنترل‌شده (`Controlled`)** | **کنترل‌نشده (`Uncontrolled`)** |  
|----------------------------|------------------------------|  
| مقدار `input` توسط `state` مدیریت می‌شود | مقدار `input` توسط `DOM` مدیریت می‌شود |  
| از `onChange` برای به‌روزرسانی استفاده می‌کند | از `ref` برای دسترسی به مقدار استفاده می‌کند |  
| مناسب برای فرم‌های پیچیده | مناسب برای فرم‌های ساده |  

### **مثال کنترل‌شده:**  
```jsx
const [value, setValue] = useState("");
return <input value={value} onChange={(e) => setValue(e.target.value)} />;
```  

### **مثال کنترل‌نشده:**  
```jsx
const inputRef = useRef();
return <input ref={inputRef} />; // مقدار با `inputRef.current.value` خوانده می‌شود
```  

---

## **۵. چرا باید کد `JSX` را transpile کنیم؟**  

مرورگرها **JSX** را نمی‌فهمند! بنابراین ابزاری مثل **Babel** آن را به **JavaScript خالص** تبدیل می‌کند:  

```jsx
// قبل از ترنسپایل:
const Greeting = () => <h1>Hello!</h1>;

// بعد از ترنسپایل:
const Greeting = () => React.createElement("h1", null, "Hello!");
```  

---

## **۶. هوک‌های (`Hooks`) ری‌اکت چه قوانینی دارند؟**  

1. **هوک‌ها را فقط در سطح بالا فراخوانی کنید** (نه در حلقه/شرط).  
2. **فقط در کامپوننت‌های تابعی یا هوک‌های سفارشی استفاده کنید**.  
3. **نام هوک‌ها باید با `use` شروع شود** (مثل `useState`, `useEffect`).  

❌ **غلط:**  
```jsx
if (condition) {
  useEffect(() => { ... }); // خطا! هوک داخل شرط است
}
```  

✅ **صحیح:**  
```jsx
useEffect(() => {
  if (condition) { ... } // هوک در سطح بالا است
}, [condition]);
```  

---

## **۷. چگونه خطاها را در ری‌اکت مدیریت کنیم؟**  

با استفاده از **`Error Boundary`**:  

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return <h1>خطایی رخ داد!</h1>;
    }
    return this.props.children;
  }
}

// استفاده:
<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>
```  

---

## **۸. React Fiber چیست؟**  

**موتور جدید ری‌اکت** برای:  
- **رندر ناهمزمان** (تقسیم کار به بخش‌های کوچک).  
- **اولویت‌بندی به‌روزرسانی‌ها** (مثلاً انیمیشن‌ها مهم‌تر از fetch داده).  

---

# **نتیجه‌گیری**  
این **۱۷ سوال** مهم‌ترین مفاهیم ری‌اکت را پوشش می‌دهند. اگر بر آنها مسلط شوید، **شانس موفقیت شما در مصاحبه‌ها بسیار افزایش می‌یابد!** 🚀  

آیا سوال دیگری دارید؟ در بخش کامنت‌ها بپرسید! 😊  

```jsx
// مثال کد نهایی برای نمایش یک کامپوننت ساده:
const App = () => (
  <div>
    <h1>مصاحبه ری‌اکت ۱۴۰۴</h1>
    <p>موفق باشید!</p>
  </div>
);
```  

**🔹 نکته:** برای انتشار در **GitHub**، این متن را در فایل `README.md` قرار دهید و از **قالب‌بندی Markdown** استفاده کنید.  

امیدوارم این راهنما مفید باشد! 🙌
