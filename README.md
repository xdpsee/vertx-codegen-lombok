# vertx-codegen 和 lombok 一起使用简化 DataObject 代码

1. 添加lombok依赖
```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.6</version>
    <scope>provided</scope>
</dependency>
```
2. maven-compiler-plugin 配置
```xml
<build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                <configuration>
                    <annotationProcessors>
                        <!-- lombok在前， 否则会出错 -->
                        <annotationProcessor>lombok.launch.AnnotationProcessorHider$AnnotationProcessor</annotationProcessor>
                        <annotationProcessor>io.vertx.codegen.CodeGenProcessor</annotationProcessor>
                    </annotationProcessors>
                    <generatedSourcesDirectory>${project.build.directory}/generated-sources/annotations</generatedSourcesDirectory>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

3. 示例
```xml
@DataObject
@Data
@NoArgsConstructor
public class Network implements Serializable {

    private static final long serialVersionUID = 6463361247973962010L;

    public Network(CellTower cellTower) {
        cellTowers.add(cellTower);
    }

    public Network(JsonObject jsonObj) {
        JsonUtils.fromJson(jsonObj, this);
    }

    public JsonObject toJson() {
        return JsonUtils.toJson(this);
    }

    // 属性
    private Integer mobileCountryCode;

    private Integer mobileNetworkCode;

    private String radioType = "gsm";

    private String carrier;

    private Boolean considerIp = false;

    private List<CellTower> cellTowers = new ArrayList<>();

    private List<WifiAccessPoint> wifiAccessPoints = new ArrayList<>();
}
```

4. enjoy it!
