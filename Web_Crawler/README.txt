https://github.com/coldicelion/Simple-Web-Crawler
# ���Ҹ�Ч����վ����

����C#.NET�ļ���ҳ���棬֧���첽���������ô�������Cookie��Gzipҳ����١�

����ͷ��@ȫջ���ܣ�[�鿴�����̳�](http://toutiao.com/a6304503113106555138/ "����ͷ��@ȫջ����")

### ��Ҫ����

- ֧��Gzip������ҳ�����Զ���ѹ���ӿ����������ٶȣ�
- ֧���첽����ץȡ��
- ֧���Զ��¼�֪ͨ��
- ֧�ִ����л�;
- ֧�ֲ���Cookies��


### ���н�ͼ	

- ץȡ�����б�

![ʹ��������ʽ��ϴ����](https://github.com/coldicelion/Simple-Web-Crawler/blob/master/Wesley.Crawler.SimpleCrawler/Images/3.%E4%BD%BF%E7%94%A8%E6%AD%A3%E5%88%99%E6%B8%85%E6%B4%97%E6%95%B0%E6%8D%AE.png?raw=true)


- ץȡ�Ƶ��б�

![ץȡ�����µľƵ��б�](https://github.com/coldicelion/Simple-Web-Crawler/blob/master/Wesley.Crawler.SimpleCrawler/Images/4.%E6%8A%93%E5%8F%96%E5%9F%8E%E5%B8%82%E4%B8%8B%E7%9A%84%E9%85%92%E5%BA%97%E5%88%97%E8%A1%A8.png?raw=true)


### ʾ������

        /// <summary>
        /// ץȡ�����б�
        /// </summary>
        public static void CityCrawler() {
            
            var cityUrl = "http://hotels.ctrip.com/citylist";//�����������URL
            var cityList = new List<City>();//���巺���б��ų������Ƽ���Ӧ�ľƵ�URL
            var cityCrawler = new SimpleCrawler();//���øղ�д���������
            cityCrawler.OnStart += (s, e) =>
            {
                Console.WriteLine("���濪ʼץȡ��ַ��" + e.Uri.ToString());
            };
            cityCrawler.OnError += (s, e) =>
            {
                Console.WriteLine("����ץȡ���ִ���" + e.Uri.ToString() + "���쳣��Ϣ��" + e.Exception.Message);
            };
            cityCrawler.OnCompleted += (s, e) =>
            {
                //ʹ��������ʽ��ϴ��ҳԴ�����е�����
                var links = Regex.Matches(e.PageSource, @"<a[^>]+href=""*(?<href>/hotel/[^>\s]+)""\s*[^>]*>(?<text>(?!.*img).*?)</a>", RegexOptions.IgnoreCase);
                foreach (Match match in links)
                {
                    var city = new City
                    {
                        CityName = match.Groups["text"].Value,
                        Uri = new Uri("http://hotels.ctrip.com" + match.Groups["href"].Value
                    )
                    };
                    if (!cityList.Contains(city)) cityList.Add(city);//�����ݼ��뵽�����б�
                    Console.WriteLine(city.CityName + "|" + city.Uri);//���������Ƽ�URL��ʾ������̨
                }
                Console.WriteLine("===============================================");
                Console.WriteLine("����ץȡ������ɣ��ϼ� " + links.Count + " �����С�");
                Console.WriteLine("��ʱ��" + e.Milliseconds + "����");
                Console.WriteLine("�̣߳�" + e.ThreadId);
                Console.WriteLine("��ַ��" + e.Uri.ToString());
            };
            cityCrawler.Start(new Uri(cityUrl)).Wait();//û�������ͱ�ʹ�ô���60.221.50.118:8090
        }

	

### ����̽��/��ϵ��ʽ

- QQ��: 276679490

- ����ܹ�����Ⱥ��180085853


