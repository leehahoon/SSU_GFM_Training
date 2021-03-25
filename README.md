# 5. HTML 태그 비활성화
GFM에서는 다음 HTML 태그를 필터링하여 HTML로 출력되지 않고, 태그 그대로 출력됩니다.

- <title>
- <textarea>
- <style>
- <xmp>
- <iframe>
- <noembed>
- <noframes>
- <script>
- <plaintext>

### 예제
```
<strong> <title> <style> <em>

<blockquote>
  <xmp> 은 필터링됩니다.  <XMP> 역시 필터링됩니다.
</blockquote>

```

### 출력
<strong> <title> <style> <em>

<blockquote>
  <xmp> 은 필터링됩니다.  <XMP> 역시 필터링됩니다.
</blockquote>
