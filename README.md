from flask import Flask, send_file
from PIL import Image

app = Flask(__name__)

@app.route('/combined_image')
def combined_image():
    # 假设这里有两张本地图片
    image1 = Image.open('image1.jpg')
    image2 = Image.open('image2.jpg')

    # 创建一个新的空白图片，用于组合
    combined = Image.new('RGB', (image1.width + image2.width, image1.height))
    combined.paste(image1, (0, 0))
    combined.paste(image2, (image1.width, 0))

    # 保存组合后的图片到临时文件
    temp_path = 'combined.jpg'
    combined.save(temp_path)

    # 返回组合后的图片
    return send_file(temp_path, mimetype='image/jpeg')

if __name__ == '__main__':
    app.run(debug=True)
