### commonmark
- commonmark是什么：是一个用来将`MarkDawn`转化`Html`的解析器
- commonmark有什么特点
    - 小：核心没有依赖关系，扩展在单独工件中
    - 快：转化效率快
    - 灵活：可以自定义`Html标签`
    - 可扩展：可添加表格、删除线等
- Java支持
    - Java8和Java9
    
### 如何使用
- 添加`pom.xml`依赖
```java
    <dependency>
            <groupId>com.atlassian.commonmark</groupId>
            <artifactId>commonmark-ext-heading-anchor</artifactId>
            <version>0.13.1</version>
        </dependency>
        <dependency>
            <groupId>com.atlassian.commonmark</groupId>
            <artifactId>commonmark-ext-gfm-tables</artifactId>
            <version>0.13.1</version>
        </dependency>
```
- 工具类
```java
    public class MarkdownUtils {

    /**
     * markdown格式转换成HTML格式
     * @param markdown
     * @return
     */
    public static String markdownToHtml(String markdown) {
        Parser parser = Parser.builder().build();
        Node document = parser.parse(markdown);
        HtmlRenderer renderer = HtmlRenderer.builder().build();
        return renderer.render(document);
    }

    /**
     * 增加扩展[标题锚点，表格生成]
     * Markdown转换成HTML
     * @param markdown
     * @return
     */
    public static String markdownToHtmlExtensions(String markdown) {
        //h标题生成id
        Set<Extension> headingAnchorExtensions = Collections.singleton(HeadingAnchorExtension.create());
        //转换table的HTML
        List<Extension> tableExtension = Arrays.asList(TablesExtension.create());
        Parser parser = Parser.builder()
                .extensions(tableExtension)
                .build();
        Node document = parser.parse(markdown);
        HtmlRenderer renderer = HtmlRenderer.builder()
                .extensions(headingAnchorExtensions)
                .extensions(tableExtension)
                .attributeProviderFactory(new AttributeProviderFactory() {
                    public AttributeProvider create(AttributeProviderContext context) {
                        return new CustomAttributeProvider();
                    }
                })
                .build();
        return renderer.render(document);
    }

    /**
     * 处理标签的属性
     */
    static class CustomAttributeProvider implements AttributeProvider {
        @Override
        public void setAttributes(Node node, String tagName, Map<String, String> attributes) {
            //改变a标签的target属性为_blank
            if (node instanceof Link) {
                attributes.put("target", "_blank");
            }
            if (node instanceof TableBlock) {
                attributes.put("class", "ui celled table");
            }
        }
    }
}
```
- 使用：调用其方法就可以了