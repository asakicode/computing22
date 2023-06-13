인공지능/ 이주형/ 20233156
# computing22















////프론트엔드
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>의료자가진단 프로그램</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
    <h1>의료자가진단 프로그램</h1>
    <div id="questionnaire">
        <h2>의료 질문</h2>
        <form id="question-form">
            <label for="q1">복통이 있나요?</label>
            <input type="checkbox" name="q1" value="복통" /><br>

            <label for="q2">열이 있나요?</label>
            <input type="checkbox" name="q2" value="열" /><br>

            <label for="q3">어지럽나요?</label>
            <input type="checkbox" name="q3" value="어지럽" /><br>

            <label for="q4">구토가 있나요?</label>
            <input type="checkbox" name="q4" value="구토" /><br>

            <button type="submit">결과 확인</button>
        </form>
    </div>

    <div id="result" style="display: none;">
        <h2>진단 결과</h2>
        <p id="result-text"></p>
    </div>

    <script>
        $(document).ready(function () {
            // 폼 제출 이벤트 핸들러
            $('#question-form').submit(function (e) {
                e.preventDefault(); // 기본 동작 중단
                var answers = [];
                $('input[type="checkbox"]:checked').each(function () {
                    answers.push($(this).val()); // 선택된 체크박스 값 배열에 추가
                });
                showResult(answers); // 결과 표시 함수 호출
            });

            // 결과 표시 함수
            function showResult(answers) {
                // 백엔드 통신 결과 받아와 로직 구현
                // 결과 생성
                var results = ["감기", "소화불량", "스트레스"];
                var randomIndex = Math.floor(Math.random() * results.length);
                var result = results[randomIndex];
                $('#result-text').text('진단 결과: ' + result);
                $('#questionnaire').hide(); // 질문 부분 숨김
                $('#result').show(); // 결과 표시
            }
        });
    </script>
</body>
</html>
////백엔드
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run()

