<!DOCTYPE html>
<html>
<body>
<script>
  // 从URL中获取code参数
  const urlParams = new URLSearchParams(window.location.search);
  const code = urlParams.get('code');
  const state = urlParams.get('state');
  
  if (code) {
    // 将code发送回打开这个窗口的扩展页面
    if (window.opener) {
      window.opener.postMessage({
        type: 'FEISHU_AUTH_SUCCESS',
        code: code,
        state: state
      }, 'https://rpa888.github.io'); // 指定源
    }
    
    // 显示提示信息并自动关闭窗口
    document.body.innerHTML = '<p>授权成功，窗口即将关闭...</p>';
    setTimeout(() => {
      window.close();
    }, 1500);
  } else {
    document.body.innerHTML = '<p>未找到授权码</p>';
  }
</script>
</body>
</html>
