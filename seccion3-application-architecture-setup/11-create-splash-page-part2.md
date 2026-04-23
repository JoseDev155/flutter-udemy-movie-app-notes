# 11. Create Splash Page | Part 2

>Continuación

En el método `build()`, vamos a retornar una nueva **MaterialApp**:

```dart
class _SplashPageState extends State<SplashPage> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flickd',
      theme: ThemeData(primarySwatch: Colors.blue),
      // Center Widget para centrar el logo
      home: Center(
        child: Container(
          height: 200,
          width: 200,
          decoration: BoxDecoration(
            image: DecorationImage(
              // Para que el logo se ajuste al tamaño del Container
              fit: BoxFit.contain,
              // Path del logo
              image: AssetImage('assets/images/logo.png')
            ),
          ),
        ),
      ),
    );
  }
}
```

Y eliminamos la carpeta de `tests/`, no la necesitamos. Y corremos la aplicación.