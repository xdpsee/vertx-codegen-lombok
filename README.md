# vertx-codegen lombok 共用

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

                      <annotationProcessor>lombok.launch.AnnotationProcessorHider$AnnotationProcessor,io.vertx.codegen.CodeGenProcessor</annotationProcessor>
                    </annotationProcessors>
                    <generatedSourcesDirectory>${project.build.directory}/generated-sources/annotations</generatedSourcesDirectory>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

3. 示例
```xml
@Data
@NoArgsConstructor
@DataObject(generateConverter = true)
public class CellTower implements Serializable {

    private static final long serialVersionUID = 1758268454928348674L;

    private String radioType;

    private Long cellId;

    private Integer locationAreaCode;

    private Integer mobileCountryCode;

    private Integer mobileNetworkCode;

    private Integer signalStrength;

    public CellTower(JsonObject jsonObj) {
        CellTowerConverter.fromJson(jsonObj, this);
    }

    public JsonObject toJson() {
        JsonObject jsonObj = new JsonObject();
        CellTowerConverter.toJson(this, jsonObj);
        return jsonObj;
    }
}
```

4. enjoy it!
