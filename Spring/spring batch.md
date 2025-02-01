## spring batch

spring batch는 대량의 데이터 처리를 위한 경량화된 프레임워크로, 반복적인 작업을 수행하는 일괄 처리 작업을 효율적으로 처리할 수 있는 기능을 제공한다. 대용량 데이터 처리나 주기적인 업무 처리 등을 효율적으로 처리할 수 있고, 대용량 데이터 처리에 적합한 분산 방식의 처리를 지원한다.

대용량 데이터 처리, 트랜잭션 관리, 재시도 기능을 제공한다.

spring batch에서 배치가 실패해서 작업을 재시작하면 실패한 지점부터 실행을 하게 된다.

또 중복 실행을 막기 위해 성공한 이력이 있는 batch는 동일한 파라미터로 실행 시 exception이 발생하게 된다.

> spring batch 용어

#### Job

job은 배치처리 과정을 하나의 단위로 만들어 놓은 객체이다.
또 배치처리 과정에 있어 전체 계층 최상단에 위치한다.

#### JobInstance

JobInstance는 Job의 실행의 단위를 나타낸다. Job을 실행시키게 되면 하나의 JobInstance가 생성된다.

#### JobParameters

JobInstance는 Job의 실행 단위라고 했다. 그렇다면 JobInstance는 어떻게 구별할까? 바로 JobParameters 객체로 구분하게 된다. JobParameters는 JobInstance 구별 외에도 개발자 JobInstance 에 전달되는 매개변수 역할도 하고 있다. 또한 JobParameters는 String, Double, Long, Date 4가지 형식만 지원한다.

#### JobExecution

JobExecution은 JobInstance에 대한 실행 시도에 대한 객체이다.

#### Step

Step은 Job의 배치처리를 정의하고 순차적인 단계를 캡슐화 한다. Job은 최소한 1개 이상의 Step을 가져야 하고, Job의 실제 일괄 처리를 제어하는 모든 정보가 들어있다.

#### StepExecution

StepExecution은 JobExecution과 동일하게 Step실행 시도에 대한 객체를 나타낸다. 하지만 Job이 여러개의 Step으로 구성되어 있을 경우 이전 단계의 Step이 실패하게 되면 다음 단계가 실행되지 않음으로 실패 이후 StepExecution은 생성되지 않는다.

#### ExecutionContext

ExecutionContext란 Job에서 데이터를 공유할 수 있는 데이터 저장소이다.

#### JobRepository

JobRepository는 위에서 말한 모든 배치 처리 정보를 담고있는 매커니즘이다.

#### JobLauncher

JobLauncher는 Job과 JobParameters를 사용하여 Job을 실행하는 객체이다.

#### ItemReader

ItemReader는 Step에서 Item을 읽어오는 인터페이스이다.

#### ItemWriter

ItemWriter는 처리 된 Data를 Writer할 때 사용한다. 

#### ItemProcessor

ItemProcessor는 Reader에서 읽어온 Item을 데이터를 처리하는 역할을 한다.
