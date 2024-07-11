## Widget

### Stateless

- 상태가 바뀌면 hot reload가 아닌 hot restart 을 해야 적용
- stateless 위젯에서 유저 인터랙션을 통한 ui 변경 logic을 작성하지 마라.
  - 만약 유저 인터랙션을 통해 내부 데이터나 상태 변경이 필요하면 callback으로 밖에서 변경해라.
- stateless가 test하기 좋다. (내부 인스턴스들이 모두 상수)
- test할 때 testWiget을 사용하는데 material과 scaffold 모두 필요하다.

- Image에서 16:9로 설정 : AspectRatio 사용

### UI Test

```dart
void main() {
  testWidgets('test text', (tester) async {
    await tester.pumpWidget(const MyApp())


    // 1번
    final titleFinder = find.text('T');
    expect(titleFinder, findsOneWidget);

    // 2번
    const testKey = Key('key'); // test를 원하는 Widget에 key를 설정해놓으면 된다.
    await tester.pumpWidget(const MyApp())
    expect(find.byKey(testKey), findOneWidget);

    expect(find.byWidget(somethingWidget, findOneWidget));

    expect(find.byType(Button), findOneWidget);
    }
  )
}
```
