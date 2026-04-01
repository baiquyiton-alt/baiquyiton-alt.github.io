[index.html](https://github.com/user-attachments/files/26419994/index.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的IP查询工具</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft YaHei", sans-serif;
        }
        body {
            background: #f5f7fa;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        .ip-card {
            background: white;
            padding: 40px;
            border-radius: 16px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 500px;
            text-align: center;
        }
        .title {
            font-size: 24px;
            color: #333;
            margin-bottom: 30px;
        }
        .ip-info {
            margin: 16px 0;
            padding: 12px;
            background: #f8f9fa;
            border-radius: 8px;
            font-size: 18px;
        }
        .label {
            color: #666;
            font-weight: bold;
        }
        .value {
            color: #2d8cf0;
            font-weight: bold;
            word-break: break-all;
        }
        #loading {
            color: #999;
            font-size: 16px;
        }
        <!-- 百度统计代码（后面替换成你自己的） -->
        <script>
            var _hmt = _hmt || [];
            (function() {
              var hm = document.createElement("script");
              hm.src = "https://hm.baidu.com/hm.js?0f796bd1aca1d4d05ce81986c2a534ac";
              var s = document.getElementsByTagName("script")[0]; 
              s.parentNode.insertBefore(hm, s);
            })();
        </script>
    </style>
</head>
<body>
    <div class="ip-card">
        <h1 class="title">🌍 访客IP信息</h1>
        <div id="loading">正在获取你的IP信息...</div>
        <div id="ipResult" style="display: none;">
            <div class="ip-info">
                <span class="label">你的IP地址：</span>
                <span class="value" id="ip"></span>
            </div>
            <div class="ip-info">
                <span class="label">IP归属地：</span>
                <span class="value" id="location"></span>
            </div>
            <div class="ip-info">
                <span class="label">运营商：</span>
                <span class="value" id="isp"></span>
            </div>
        </div>
    </div>

    <script>
        // 获取访客IP和归属地
        fetch('https://api.ip.sb/geoip')
            .then(res => res.json())
            .then(data => {
                document.getElementById('loading').style.display = 'none';
                document.getElementById('ipResult').style.display = 'block';
                
                document.getElementById('ip').textContent = data.ip;
                document.getElementById('location').textContent = 
                    `${data.country || ''} ${data.region || ''} ${data.city || ''}`.trim();
                document.getElementById('isp').textContent = data.isp || '未知';
            })
            .catch(err => {
                document.getElementById('loading').textContent = '获取失败，请刷新重试';
                console.error(err);
            });
    </script>
</body>
</html>
